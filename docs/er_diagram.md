# Entity Relationship (ER) Diagram

This diagram represents the relationships between key entities in the Job Portal App database.

```mermaid
erDiagram
	
    USER {
        string _id
        string fullname
        string email
        string password
        string role "student | recruiter"

        %% Profile Section (Nested Fields)
        string[] profile_skills
        string profile_resume "resume file URL"
        string profile_resumeOriginalName
        string profile_profilePhoto

        string createdAt
    }
	JOB {
		string _id  ""  
		string title  ""  
		string description  ""  
		string[] requirements  ""  
		number salary  ""  
		number experienceLevel  ""  
		string location  ""  
		string jobType  ""  
		number positions  ""  
		string company  ""  
		string created_by  "User._id"  
		string[] applications  "Array of Application._id"  
		string createdAt  ""  
	}
	APPLICATION {
		string _id  ""  
		string job  "Job._id"  
		string applicant  "User._id"  
		string status  "pending | under_review | shortlisted | accepted | rejected"  
		string createdAt  ""  
	}
	USER||--o{JOB:"creates"
	USER||--o{APPLICATION:"applies"
	JOB||--o{APPLICATION:"receives"


```
