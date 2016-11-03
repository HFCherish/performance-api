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

	
	
	
	
==================================================================

# /users/uid/self_reflections
* post
	* return 201 when create new self relfection for some user
	* save to db and can get that self_reflection later
	* contains url in location

	* return 400 when behavior empty;

	* return 403 when current user is not consistent with uid
* get
	* return 200 when get all the self_reflections;
	* try to search db and can get the right one from db;
	* contains right count, page, items (id, createdat, competence, behavior, links, owner, creator) info;

	* return 403 when not uid or not admin

# /users/uid/self_reflections/srId
* get
	* return 200 when get one self_reflection;
	* contains right id, createdat, competence, behavior, links, owner, creator in response;
	* 
	* return 404 when not exists;

	* return 403 when not uid or not admin

# can create more than one self reflections at one time.

# /users/uid/self_reflections/srId/evidences
* post
	* return 201 when create new evidence for some user
	* save to db and can get that evidence later
	* contains url in location

	* return 400 when content, witness empty;

	* return 403 when is not consitent with uid

# /users/uid/self_reflections/srId/evidences/eid
* get
	* return 200 when get one evidence;
	* contains right id, content, links in response;
	* 
	* return 404 when not exists;

	* return 403 when not owner of self_reflection or not witness of the this evidence or not admin

# contains right evidences info when get self_reflections (get all & get one)

# save witnesses and feedbacks when create evidence
    * save witnesses to db
	* save feedbacks for each witness to db

# /users/uid/self_reflections/srId/evidences/eid/feedbacks/fid
* put
	* return 204 when update feedbacks
	* update db

	* return 400 when approved, comment empty;

	* return 404 when the feedback does not exists for this evidence

	* return 403 when current user is not the author of this fid

# contains right feedbacks info when get evidence



# /programs/id/assignments
* post
	* return 201 when assign
	* try to save to and can get that one from db;
	* contains url

	* return 400 when not contains username, role, coach
* get
	* return 200 when get assignments of this program;
	* search from db
	* contains right username, nickname, id, role, coach,  programId

# /programs/id/assignments/aid
* delete
	* return 204 when delete an assignment
	* delete from db;

	* return 404 when not exists;
===========================================
# /users/uid/assignments
* get
	* return 200 when get all assignments of some user
	* search from db
	* contains right details

	* return 403 when the current user is not same as uid user, or not admin

# return 403 when create self_reflection if current user is not uid or not coach of uid.

# /users/uid/programs/pid/evidences
* put
	* return 204 when set evidences for program
	* delete all evidences of this user and program. save new evidences to db

	* return 400 when evidences empty

	* return 403 when current user is not consitent with uid
	* return 403 when current user is in the program but is not coachee
	* 
	* return 404 when program not published
* get
	* return 200 when get evidences of user for program
	* search from db and can get the right one
	* contains right details

	* return 403 when not uid or not coach of this user or not admin

	* return 404 when program not published
	* return 404 when current user is not in the program

# delete support of user/uid/program/pid/assignments

# modify the return info when get user assignments

# can post assignment through assignments rather that program/pid/assignments

# can get assignment through assignments rather that program/pid/assignments

# can delete assignment through assignments/aid rather than program/pid/assignments/aid

# delete feedbacks when delete witness assignment

# contains right info when get assignments

# contains right info when get evidence

# can update evidence

# can batch create assignments

# can get assignments by query (role array, program)
* for witness assignments, can get evidences info by query parameter

# can get program evidences by query parameter (time, owner, program)
* filter by time

# coach can view and create the self reflection of coachee

# delete support for config and get evidences in program

# contains category info whenever get competence

# admin can get all user/uid/assignments, including unpublished program. normal user can only get assignments of published program

# config email

# when show evidence data, show behavior outside

# when show assignment data,
* show behavior outside
* show feedback outside

# when show selfReflection data, show behavior outside

# get user evidences filtered by
* date,
* behaviors,

# show evidences in page
* when get user evidences
* when get all evidences

# get self confidences filtered by
* isComplete

# delete evidence
* delete witness cascade
* decrease self reflection evidence count

# create new table for witness
* save and get witnesses to and from new table

# can get all coachees of somebody

# move add/get/delete assignment under program
* add/get/delete assignment through program

# one selfReflection should gather a group of patterns, and each pattern contains several evidences
* save: modify self reflection table
* get: contains right info.

# can get all categories

# contains right info for evidence

# refactor: should an feedback update and delete itself

# modify evidence api to add pattern field rather than use it in api

# assignment 500

# save assignment using object and check the constraint.

# hint is required when create or update pattern

# user img info

# delete using delete tag rather than delete physically for: evidence, category, competence, pattern, program, programCompetence
* category
* competence
* pattern
* evidence
* program
* programCompetence

# recheck the cascade delete before

# check all foreign key constraint
* check the validity of the assignments (username, coachName,
    * when create evidence (witness assignments)
    * when assign

# delete unused classes

# modify feedback user in mybatis using prefix

# when state evidence and invite observer, save the invitations
* save observer invitations
* save coach invitations

# can submit evidence
* send email when publish evidence.
* when get all evidences (of user or by admin), can only get submitted evidences
* when get an evidence, show all for author, and show submitted evidences for observers and coaches
* when get self_reflection(s), show all evidence for author and submitted evidences for others
* when get all user evidences, coach and itself can get user evidence.

# modify invitations info
* show program info for coach type invitation.
* delete comment, approved info
* the id should be invitation id
* show evidence link
* modify invitation link (.../feedbacks)

# can post feedback (comment, endorsed)
* only the observers and coaches can post feedback for the evidence

# when get evidence info with feedbacks, contains program and role info for feedback.
* modify feedback table (id, invitationId, comment, approved, createdAt)
* feedback default false, which means it's not endorsed

# can delete feedback
* can only delete feedback of yourself (admin can delete too)

# when put evidence, provide witnesses list
* can only update before submit

# contains observers info for evidence

# for feedback info, contains detail program info

# add endorsed type feedback
* when post feedback, contains type info. and comment is required for Comment type feedback;
* when post feedback, for endoresed type feedback, delete first and then save.
* when get feedbacks info, contains different type feedback info.

# contains different lin./ks info when get evidence for different user

# self can give feedback, too.





# decide if self_reflection and evidence is in one aggregate

# reorganize the domain folder to show the true domain -- elaborate the model using module

# decide if state evidence should be in service -- what should be described using service

# check the isComplete filter because now the feedback has changed
* for self_reflection, why don't we need the isComplete? If needed, it is complete when at least one evidence is submitted

# decide if use event to save all invitations

# use jwt to authenticate

# use obj to save


