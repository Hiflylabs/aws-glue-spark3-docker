This repository is forked from https://github.com/alrouen/local-aws-glue-v3-zeppelin 

# Build docker image

    cd docker
    docker build -t gluedev . 

# Run image

    docker run -d --rm --name gluedev -p 8080:8080 -p 7077:7077 -p 9001:9001 -v $PWD/logs:/logs -v $PWD/notebook:/notebook -e ZEPPELIN_LOG_DIR='/logs' -e ZEPPELIN_NOTEBOOK_DIR='/notebook' -v /path/to/your/.aws:/root/.aws:ro gluedev

The .aws volume is only required if you want your local job to get access to your AWS environment (ie. bucket S3).

# Zeppelin access

    http://localhost:9001
    
# S3 access :

To enable AWS S3 access with your AWS credential just add this line in your notebook :

    spark.sparkContext._jsc.hadoopConfiguration().set("fs.s3a.aws.credentials.provider", "com.amazonaws.auth.DefaultAWSCredentialsProviderChain")
    
(source: http://wrschneider.github.io/2019/02/02/spark-credentials-file.html)
