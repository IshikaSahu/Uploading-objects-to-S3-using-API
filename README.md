#Uploading-objects-to-S3-using-API

#Let's first create a bucket in s3 aws cloud service

So for creating a bucket we need to go to s3 service and click on create bucket a page will look like this:
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/10159c0f-8416-44a5-a900-ab4801b06c56)
give your unique bucket name let say ishika-b-01 and click on create bucket.
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/cfd3c3c3-c041-406e-b432-afd03b407df1)


#Now as your bucket is ready let's go and make an api gateway to upload object in s3 using api

Go to service api gateway in aws cloud and click on create api and then click on build button of 3rd option Rest Api. The page will look like this:
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/b6ec3907-d6d2-4e2d-8757-1a69fcb404a0)
give api name and click on create and then go on action option and create resource
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/b6c8f9f5-c544-42fa-a3e9-cd903934b571)
give resource name and then click on create button 
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/555489f3-3736-436f-b9f0-00cb47c329b2)
then create another resource and give variable over there i gave it {myfile} and click on create
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/2284f2f2-0b73-46d1-ba68-5f7f1f56c895)
Now we will create method for uploading file using api then go to action and click on create method and choose put and click on tick button
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/9c08012d-cef9-4f1e-9c1f-ea129a7eac41)
Now choose 
Integration type : aws service
aws region : bucket region
aws service : s3
HTTP method : PUT
Action Type : Use path override
path override : bucket-name/{variable}   in my case (ishika-b-01/{method})

Now here one problem came as api will hit there will be somthing that we are going to upload so that means api gateway need to contact s3 service for which there is required a role to create between them for authentication purpose so we will now go on IAM service in aws cloud and then we will go on roles and create a new role. We will choose api gateway in use case and click on next 
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/783a9b12-b3d6-415e-8575-73ec1516e91b)
again go to next and give role name and click on create role now go inside of your role
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/02e80c96-1824-4963-82bd-ac56cb57608e)
now click on add permissions and the attach policies and the attach a policy name AmazonS3FullAccess
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/21b36583-82e1-4b46-a3af-b49bbc90de8a)
click on add permissions now copy arn number of that role and come back to api gateway service and paste the value of 
execution role : arn:aws:iam::326047316803:role/apipermissiontos3
click on save 

now come on integration service and go down you will find url path parameters add path over there
Name                           Mapped from
variable name (method)         method.request.path.myfile
click on tick button
now go in settings and come down you will see one option called binarymedia types give there */* which means accept files of all type and click on save changes
Now come on resources again and go to actions and click on deploy api ang give state name and click on deploy
![image](https://github.com/IshikaSahu/Uploading-objects-to-S3-using-API/assets/71627396/d4ae7721-1d27-4ed7-98c4-562726f95348)
Now use curl command and run it.




 
