Creates an all in one jar for deploying 3rd party artifacts to an S3 repository. To use:

1. Build the jar with by running 'mvn clean assembly:single'

2. Copy the jar from target into $M2_HOME/lib

3. Add your S3 credentials to ~/.m2/settings.xml. The password should NOT be encrypted. Example:

```xml
<servers>
	<server>
		<id>s3-maven-repo</id>
		<username>[S3_USERNAME]</username>
		<password>[S3_PASSWORD]</password>
	</server>
</servers>
```

4. cd to the directory of the artifacts that you want to deploy, then use deploy:deploy-file like this.

mvn deploy:deploy-file -Dfile=java-aws-mturk.jar -DgroupId=com.amazon -DartifactId=java-aws-mturk -Dversion=1.2.2 -Dpackaging=jar -DrepositoryId=s3-maven-repo -Durl=s3://s3-maven-repo/repo -DuniqueVersion=false