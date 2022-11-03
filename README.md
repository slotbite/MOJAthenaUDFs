# MOJAthenaUDFs
### AWS ATHENA UDFs for Record Linkage

Need Java 1.8 / Maven installed. Installation of both through SDKMAN is recommended



### HOW TO BUILD JAR:


    mvn package clean #to check if it compiles
    mvn clean install -DskipTests

Create a lambda function (make sure that lambda role is created before this)

    aws lambda create-function
    --function-name athenaudf
    --runtime java8
    --role arn:aws:iam::3242345446345:role/serverlessrepo-AthenaUserDefin
    --handler com.awssupport.athena.udfs.MOJAthenaUserDefinedFunctions
    --timeout 900
    --zip-file fileb://./target/MOJAthenaUserDefinedFunctions-1.0-SNAPSHOT --region eu-west-1

Go to Athena and make sure that Console is pointing to Engine version 2

Run below query to test UDF

`USING EXTERNAL FUNCTION compress(input VARCHAR) RETURNS VARCHAR LAMBDA 'athenaudf' SELECT compress('Hello')`

---
### Progress

v.1.0.0

get this mechanism working / compiling and outputing a jar. 
Next step: Test that its working on Athena.

- double metaphone should be ready and working
- Jaro Winkler from Apache Commons also compiles sucessfully but currently need to make it scalar , in the way UDFs Athena expect



---
### References

[1] [Athena querying udfs](https://docs.aws.amazon.com/athena/latest/ug/querying-udf.html)

[2] [Athena UDFs: creating and deploying](https://docs.aws.amazon.com/athena/latest/ug/querying-udf.html#udf-creating-and-deploying)

[3] [AWS Athena UDF access to lambda context](https://stackoverflow.com/questions/70128935/aws-athena-udf-access-to-lambda-context)

