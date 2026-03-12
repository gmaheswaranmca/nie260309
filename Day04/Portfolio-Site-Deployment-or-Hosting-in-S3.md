To make my portfolio site live using AWS S3 Service:
1. Create Bucket 
	[] General Purpose Bucket 
	Name: [ arjun-sharma-nie-campus]
	Untick "Block all public access"
	Tick "I acknowledge that the current settings might result in this bucket and the objects within becoming public."
	-> "Create Bucket" at Bottom Right Corner
2. Open bucket "arjun-sharma-nie-campus"
	Properties
	-> Static website hosting
	-> Edit 
	-> Static Website Hosting 
		[Tick] Enable
	-> Index Document: index.html
	-> Error Document: error.html 
	-> Save Changes
3. Open bucket "arjun-sharma-nie-campus"
	-> Objects
	-> Upload 
	-> Add Files or Add Folder 
		index.html 
		etc
	-> Upload 
4. Open bucket "arjun-sharma-nie-campus"
	-> Permissions 
	-> Bucket policy
	-> Edit 
	Policy is as follows: (Note change your bucket name here)	
	{
	"Version":"2012-10-17",
	"Statement":[
	{
	"Sid":"PublicRead",
	"Effect":"Allow",
	"Principal":"*",
	"Action":["s3:GetObject"],
	"Resource":["arn:aws:s3:::arjun-sharma-nie-campus/*"]
	}
	]
	}
	-> Save Changes 
5. Open bucket "arjun-sharma-nie-campus"
	-> Properties 
	-> Static website hosting
	-> Bucket website endpoint
		Open or Click "http://arjun-sharma-nie-campus.s3-website.ap-south-1.amazonaws.com"
Now we will see our portfolio site. 
