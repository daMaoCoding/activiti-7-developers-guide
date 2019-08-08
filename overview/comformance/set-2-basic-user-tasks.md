# BPMN Comformance Set 2

This scenario checks User Tasks and basic assignments properties. It also check the events generated by the Task Runtime. Task Operations are used to interact against Task resources. The [source code of these tests can be found here](https://github.com/Activiti/Activiti/tree/develop/activiti-spring-conformance-tests/activiti-spring-conformance-set2).

![](../../.gitbook/assets/set-2-user-task.png)

* [User Task with User Assignment](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20Assignee.bpmn20.xml) 
  * We should be able to start the process and check that the Status after start is RUNNING
  * This process instance has a concrete assignee: “user1”
  * We should query for the tasks for the assigned user and check that we get just one task
  * We should check that User2 doesn’t have any task
  * We should be able to get the task by id using User1 
  * **Start Process Operation**: 
    * PROCESS\_CREATED
    * PROCESS\_STARTED
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * TASK\_CREATED
    * TASK\_ASSIGNED
    * TASK\_UPDATED
  * User1 should be able to complete the task    
  * **Task Complete Operation**
    * TASK\_COMPLETED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * PROCESS\_COMPLETED
* [User Task with Candidate User](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20CandidateUser.bpmn20.xml)
  * We should be able to start the process and check that the Status after start is RUNNING
  * This process instance has no concrete assignee
  * We should query for the tasks for the candidate user and check that we get just one task
  * We should check that User2 doesn’t have any task
  * We should be able to get the task by id using User1 
  * We should check that User2 cannot get the task by id
  * Neither User1 or User2 should be able to complete the task before having an assignee set \(different errors User2 not found, User1 cannot complete without assignee\)
  * User1 should be able to claim the task
  * After claim the assignee should be set
  * If User1 is an assignee he/she should be able to complete the task
  * We should check that the assignee was removed after release
  * **Start Process Operation**:
    * PROCESS\_CREATED
    * PROCESS\_STARTED
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * TASK\_CREATED
  * We should get the following events after claiming the task
  * **Claim Task Operation**:
    * TASK\_ASSIGNED
    * TASK\_UPDATED
  * We should get the following events after releasing the task
  * **Release Task Operation**: 
    * TASK\_COMPLETED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * PROCESS\_COMPLETED
* [User Task with Candidate User Claim & Release Task](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20CandidateUser.bpmn20.xml)
  * We should be able to start the process and check that the Status after start is RUNNING
  * **Start Process Operation**
    * PROCESS\_CREATED
    * PROCESS\_STARTED
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * TASK\_CREATED
  * This process instance has no concrete assignee
  * We should query for the tasks for the candidate user and check that we get just one task
  * We should check that User2 doesn’t have any task
  * User1 should be able to claim the task
  * The task status should be ASSIGNED
  * User1 should be able to release the task
  * The task status should be CREATED
  * **Claim Task Operation**
    * TASK\_ASSIGNED
    * TASK\_UPDATED
  * **Release Task Operation**
    * TASK\_ASSIGNED
    * TASK\_UPDATED
* [User Task with Candidate Group](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20CandidateGroup.bpmn20.xml)
  * We should be able to start the process and check that the Status after start is RUNNING
  * This process instance has no concrete assignee
  * We should query for the tasks for the candidate group Group1, User1 and User3 get one task
  * We should check that User2 doesn’t have any task
  * We should be able to get the task by id using User1 and User3
  * We should check that User2 cannot get the task by id
  * Neither User1 or User2 should be able to complete the task before having an assignee set
  * User1 should claim the task
  * User3 will no longer see that task because it was assigned to User1
  * **Start Process Operation**
    * PROCESS\_CREATED
    * PROCESS\_STARTED
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * TASK\_CREATED
  * **Claim Task Operation**
    * TASK\_ASSIGNED
    * TASK\_UPDATED
  * **Release Task Operation**
    * TASK\_COMPLETED,
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * PROCESS\_COMPLETED
* [User Task with Candidate Group Claim & Release Task](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20CandidateGroup.bpmn20.xml)
  * We should be able to start the process and check that the Status after start is RUNNING
  * **Start Process Operation**
    * PROCESS\_CREATED
    * PROCESS\_STARTED
    * ACTIVITY\_STARTED
    * ACTIVITY\_COMPLETED
    * SEQUENCE\_FLOW\_TAKEN
    * ACTIVITY\_STARTED
    * TASK\_CREATED
  * This process instance has no concrete assignee
  * We should query for the tasks for the candidate user and check that we get just one task
  * We should check that User2 doesn’t have any task
  * We should be able to get the task by id using User1 
  * We should check that User2 cannot get the task by id
  * Neither User1 or User2 should be able to complete the task before having an assignee set
  * **Claim Task Operation**
    * TASK\_ASSIGNED
    * TASK\_UPDATED
  * **Release Task Operation**
    * TASK\_ASSIGNED
    * TASK\_UPDATED
  * User3 and User1 should be able to see the task again after release
* [User Task without Assignments](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20no%20User%20or%20Group%20Assignment.bpmn20.xml)
  * We should be able to start the process and check that the Status after start is RUNNING
  * Neither User1 or User2 should be able to see any task, due the task has no assignee, candidateUser or candidateGroup
  * A user with **ACTIVITI\_ADMIN** role should be able to see the task, but more on Admins later
* [User Task For Assignee Delete](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20Assignee.bpmn20.xml)
  * A process creates a task and the user execute delete on it
  * The user is the assignee of the task, so no need to claim
  * Calling delete on a task that belongs to a process should produce an ActivitiException: “The task cannot be deleted because is part of a running process”
* [User Task For Candidate Delete](https://github.com/salaboy/bpmn-scenarios/blob/master/processes/UserTask%20with%20CandidateUser.bpmn20.xml)
  * A process creates a task and the user execute delete on it
  * The user is the candidate of the task
  * Calling delete on a task that belongs to a process should produce an **ActivitiException**
* [User Task Details](set-2-basic-user-tasks.md) TBD
* [User Task With Data / Variables](set-2-basic-user-tasks.md) TBD
