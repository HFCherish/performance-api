# keep the following api:
1. /authentication, 
2. /users, 
3. /users/username, 
4. /users/username/password, 
5. /categories, 
6. /categories/{categoryId}

# /users, /users/username
* get
	* modify role field as array
	* can get grade info as well

# /competences
* post
	* post roleDescriptions rather than description
	* post behavior with grade

	* return 400 when name, category, roleDescriptions empty;

	* return 403 when not admin;
* get
	* can get right roleDescription and behavior with grade info
	* can filtered by role

# /competences/id
* put
	* put roleDescriptions rather than description
	* put behavior with grade

	* return 400 when name, category, roleDescriptions empty;

	* return 403 when not admin;

# /programs
* post
	* post startDate and endDate info
	
	* return 400 when name, description are empty;

	* return 403 when not admin

	* save program competences at the same time
* get
	* contains startDate and endDate info

	* return 403 when not admin 

# /programs/id
* get
	* contains competences info
	
	* return 404 when not exists;

	* return 403 when not admin 
* put
	* post startDate and endDate info
	* save program competences at the same time
	
	* return 400 when name, description are empty;

	* return 403 when not admin
	
	* return 404 when try to update a program not exists;

# /users/{username}/programs
* at present, same as get all programs

# /users/{username}/programs/{programId}/assignments
* post: can post sponsor / project_leader type assignments 
	* return 201 when assign
	* try to save to and can get that one from db;
	* contains url

	* return 400 when not contains required fields

	* return 403 when current user not {username}
* get: can get all assignments assigned by {username}
	* return 200 when get assignments of this program;
	* search from db
	* contains right username, nickname, id, role, coach,  programId

	* return 403 when current user not {username} or not admin

# /users/{username}/programs/{programId}/assignments/{aid}
* delete
	* modify the path

	* return 403 when current user not {username};

# /users/{username}/programs/{programId}/self_reviews
* post
	* modify the path
	* add program field for self review table

	* return 400 when behavior empty;
	* return 400 when the behavior is not in the program

	* return 403 when current user is not {username}
* get
	* contains right program, competences, links info

	* return 403 when not uid or not admin or not sponsor or not project lead

	* for people who are not {username} can only get self review with submitted evidence

# /users/{username}/programs/{pid}/self_reviews/srId
* get
	* contains right program, competences info
	
	* return 404 when not exists;

	* return 403 when not uid or not admin

# /users/{username}/programs/{pid}/self_reviews/srId/invitations
* post
	* return 201 when invite observers
	* try to save to and can get that one from db;
	* contains url

	* return 400 when not contains required fields

	* return 403 when current user not {username}

	* send email to these observers and sponsor and project leads

# contains right observers info when get one self_review

# /users/{username}/programs/{programId}/self_reviews/{srId}/feedbacks
* post
	* return 201 when create feedback
	* try to save to and can get that one from db;
	* contains url

	* return 400 when not contains required fields
	* return 400 when competence is not exists or not in the program

	* return 403 when current user not sponsor, observer or project lead of {username}

# /users/{username}/programs/{programId}/self_reviews/{srId}/feedbacks/{fid}
* delete
	* return 204 when delete feedback
	* delete from db

	* return 404 when the feedback does not exists for this self_review

	* return 403 when current user is not the author of this fid

# contains right feedbacks info when get one self_review

# contains only feedback of self when get one self_review by observer

# /users/{username}/programs/{programId}/self_reviews/{srId}/evidences
* post
	* do not contains observers info when post evidence

	* return 400 when content, behavior empty;
	* return 400 when the behavior is not belongs to this self review

	* return 403 when current user is not {username}

# /users/{username}/programs/{programId}/self_reviews/{srId}/evidences/{eid}
* put
	* return 204 when update evidence
	* udpate from db

	* return 404 when the evidence does not exists for this self_review

	* return 403 when current user is not {username}
	
	* return 409 when the evidence has been submitted
* delete
	* modify the path
* /submit
	* modify the path	

# contains right evidences info when get one self_review

# /users/{username}/invitations
* get
	* can get all invitations of {username} with right info

	* return 403 when current user is not {username}

# remind the observer, project lead, sponsor when they haven't given feedback 5 days before the deadline of program