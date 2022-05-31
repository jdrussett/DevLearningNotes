# Asynchronous Apex

## General

---

Common uses of asynchronous Apex (tasks finish in the background, don't have to wait for different executions to finish) include:

- Callouts to external systems
- Operations that require higher limits
- Code that needs to be run on time-specific basis

Benefits of asynchronous Apex:

- User efficiency
- Scalability
- Higher limits

Various types of asynchronous Apex exist:

| **Type** | **Overview** | **Common Scenarios** |
| --- | --- | --- |
| **Future Methods** | Run in their own thread, do not start until resources are available | Web service callouts |
| **Batch Apex** | Run large jobs that would exceed normal processing limits | Data cleansing, archiving old records |
| **Queueable Apex** | Similar to future methods, provide additional job chaining, allow more complex data types to be used | Performing sequential processing operations with external web services |
| **Scheduled Apex** | Schedule Apex to run at a specified time | Daily/weekly tasks |

Governor/execution limits are increased with asynchronous Apex  

Platform uses queue-based asynchronous processing framework; used to manage asynchronous requests for multiple orgs within each instance

> Lifecycle made up of 3 parts:
>
> 1. Enqueue - request is put into queue; Apex batch request, future Apex request, etc.; platform will enqueue requests along with appropriate data to process the request
> 2. Persistence - request is persisted; stored in persistent storage for failure recovery & to provide transactional capabilities
> 3. Dequeue - request is removed from queue & is processed; transaction management occurs in this step

Can't use `getContent()` or `getContentAsPDF()` methods in any future Apex method

Future classes must be annotated with `@future(callout=true)` and must be static and only return type of void

## Batch Apex

---

To write batch Apex, class must implement `Database.Batchable` interface & include each of the following 3 methods:

1. `start`
2. `execute`
   - Takes in reference to Database.BatchableContext object
   - Takes in list of sObjects or parameterized types
3. `finish`

Outline of a batch Apex class:

    global class batch_class_name implements Database.Batchable<sObject> {
        global (Database.QueryLocator [OR] Iterable<sObject>) start(Database.BatchableContext bc) {
            // ... collect the batches of records or objects to be passed to execute ...
        }
        global void execute(Database.BatchableContext bc, List<P> records){
            // ... process each batch of records ...
        }
        global void finish(Database.BatchableContext bc){
            // ... execute any post-processing operations ...
        }
    }

**Invoke batch Apex** class by instantiating it & calling `Database.executeBatch` with the instance

> Example:
>
>        batch_class_name batch_object = new batch_class_name();
>        Id batch_id = Database.executeBatch(batch_object, batch_size_integer);
>
> - Optional scope parameter specifies number of records to be passed into the execute method for each batch

Each batch Apex invocation produces `AsyncApexJob` record to let you track job's progress

> View progress of a particular job with the following SOQL query:
>
>       AsyncApexJob job_var = [Select Id, Status, JobItemsProcessed, TotalJobItems, NumberOfErrors 
>                               From AsyncApexJob
>                               Where Id = :batch_id];

Including `Database.Stateful` in class definition lets you maintain state across all transactions within batch Apex execution

- Instance member variables retain value between transactions; usful for counting/summarizing records as they're processed

## Queueable Apex

---

Called by System.enqueueJob() method

- Returns job ID you can monitor

Queueable Apex syntax:

    public class class_name implements Queueable {
       public void method_name(QueueableContext context) {
          // ... code to execute ...
       }
    }

Testing queueable Apex incorporates the startTest() and stopTest() methods just like testing batch Apex does

> Use `Test.isRunningTest()` to see if Apex is running when testing queueable Apex

- Can't chain queueable jobs together for testing purposes

## Schedulable Apex

---

Schedulable Apex syntax:

    global class class_name implements Schedulable {
       global void execute(SchedulableContext sc) {
          ... code to execute ...
       }
    }

`System.schedule` method executes a schedulable class, which you implement with `Schedulable` interface in the class definition

- Takes 3 arguments:
  1. Name for job
  2. CRON expression used to represent time/date job is scheduled to run
  3. Name of schedulable Apex class
