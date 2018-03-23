
Configuring Medic Mobile
------------------------------
<!-- TOC depthFrom:1 depthTo:3 -->

- [Introduction](#introduction)
    - [What is Medic Mobile <!-- TODO: Jill to fill in with conceptual info about app, not specific to a technical audience -->](#what-is-medic-mobile----todo-jill-to-fill-in-with-conceptual-info-about-app-not-specific-to-a-technical-audience---)
        - [Review of app structure and workflows](#review-of-app-structure-and-workflows)
        - [Overview of various pages + core functions](#overview-of-various-pages--core-functions)
    - [What’s configurable <!-- TODO: Jill to fill in with list of screenshots, with notes on what is configurable in each  -->](#whats-configurable----todo-jill-to-fill-in-with-list-of-screenshots-with-notes-on-what-is-configurable-in-each----)
- [Getting Started <!-- TODO: Marc by March 30, 2018  -->](#getting-started----todo-marc-by-march-30-2018----)
    - [Prerequisite knowledge - To know before starting](#prerequisite-knowledge---to-know-before-starting)
        - [CouchDB](#couchdb)
        - [Javascript](#javascript)
        - [JSON](#json)
        - [XLSForms and XForms](#xlsforms-and-xforms)
    - [To do before starting](#to-do-before-starting)
        - [Have access to an instance](#have-access-to-an-instance)
        - [Set up a dev instance](#set-up-a-dev-instance)
        - [Set up medic-conf](#set-up-medic-conf)
- [Configure <!-- TODO: Marc by March 30, 2018 -->](#configure----todo-marc-by-march-30-2018---)
    - [Overview](#overview)
        - [File structure](#file-structure)
        - [App settings](#app-settings)
        - [...and more!](#and-more)
    - [Localization <!-- TODO: Marc by March 30, 2018, to be further fleshed out by Derick as needed -->](#localization----todo-marc-by-march-30-2018-to-be-further-fleshed-out-by-derick-as-needed---)
    - [Icons <!-- TODO: Derick -->](#icons----todo-derick---)
    - [SMS Forms](#sms-forms)
    - [App Forms <!-- TODO: review content and add subsections -->](#app-forms----todo-review-content-and-add-subsections---)
        - [Structuring a form](#structuring-a-form)
        - [Showing a form <!-- TODO -->](#showing-a-form----todo---)
        - [Getting data into a form <!-- TODO -->](#getting-data-into-a-form----todo---)
        - [Uploading forms <!-- TODO -->](#uploading-forms----todo---)
        - [Other Medic specific XForm conventions](#other-medic-specific-xform-conventions)
        - [Tips & Tricks <!-- TODO -->](#tips--tricks----todo---)
        - [Troubleshooting <!-- TODO -->](#troubleshooting----todo---)
    - [Collect Forms](#collect-forms)
    - [Profiles](#profiles)
        - [Overview](#overview-1)
        - [Info card](#info-card)
        - [Condition cards](#condition-cards)
        - [History](#history)
        - [Tasks](#tasks)
        - [Actions](#actions)
    - [Tasks <!-- TODO: Already rewritten, needs review and updated screenshots -->](#tasks----todo-already-rewritten-needs-review-and-updated-screenshots---)
        - [Configuration: `rules.nools.js`](#configuration-rulesnoolsjs)
        - [Uploading <!-- TODO -->](#uploading----todo---)
        - [Examples](#examples)
        - [Tips & Tricks](#tips--tricks)
        - [Troubleshooting](#troubleshooting)
    - [Targets <!-- TODO: Marc to revise to similar structure as Tasks -->](#targets----todo-marc-to-revise-to-similar-structure-as-tasks---)
        - [Template: `targets.json`](#template-targetsjson)
        - [Creation: `rules.nools.js`](#creation-rulesnoolsjs)
        - [Uploading <!-- TODO -->](#uploading----todo----1)
        - [Examples](#examples-1)
        - [Tips & Tricks](#tips--tricks-1)
        - [Troubleshooting](#troubleshooting-1)
- [Set-up](#set-up)
    - [Contacts](#contacts)
        - [Create [via UI, needs training module]](#create-via-ui-needs-training-module)
        - [Edit [via UI, needs training module]](#edit-via-ui-needs-training-module)
        - [Bulk create](#bulk-create)
    - [Users](#users)
        - [Overview](#overview-2)
        - [Create [via UI, needs training module] <!-- TODO: Jill -->](#create-via-ui-needs-training-module----todo-jill---)
        - [Bulk Creation (conf#61)](#bulk-creation-conf61)
        - [Permissions <!-- TODO: Derick -->](#permissions----todo-derick---)
    - [Data Migration](#data-migration)
- [Deploy + Maintain](#deploy--maintain)
    - [Versioning](#versioning)
    - [Upgrades](#upgrades)
    - [Release notes](#release-notes)
    - [Deploying](#deploying)
    - [Local](#local)
    - [Development Setup](#development-setup)
    - [Contributing code](#contributing-code)
    - [Export](#export)

<!-- /TOC -->
# Introduction 
## What is Medic Mobile <!-- TODO: Jill to fill in with conceptual info about app, not specific to a technical audience -->
### Review of app structure and workflows
### Overview of various pages + core functions
#### Tasks tab
#### People tab
##### Hierarchy levels
##### People profile
###### info card
###### condition card
###### tasks
###### history
##### Place profiles
###### info card
###### (condition card)
###### sub places/people
###### tasks
###### history
#### Targets tab
##### widgets
#### History/Reports. 
##### Define Forms and where they live.
#### Definitions
## What’s configurable <!-- TODO: Jill to fill in with list of screenshots, with notes on what is configurable in each  -->
------------------------------------
# Getting Started <!-- TODO: Marc by March 30, 2018  -->
## Prerequisite knowledge - To know before starting
### CouchDB
### Javascript
### JSON
### XLSForms and XForms
## To do before starting
### Have access to an instance
### Set up a dev instance
### Set up medic-conf
------------------------------------
# Configure <!-- TODO: Marc by March 30, 2018 -->
## Overview
### File structure
### App settings
### ...and more!
------------------------------------
## Localization <!-- TODO: Marc by March 30, 2018, to be further fleshed out by Derick as needed -->
------------------------------------
## Icons <!-- TODO: Derick -->
------------------------------------
## SMS Forms
------------------------------------
## App Forms <!-- TODO: review content and add subsections -->
Whether using Medic Mobile in the browser or via the Android app, all Actions, Tasks, Contact creation/edit forms are created using [ODK XForms](https://opendatakit.github.io/xforms-spec/) -- a XML definition of the structure and format for a set of questions. Since writing raw XML can be tedious, we suggest creating the forms using the [XLSForm standard](http://xlsform.org/), and using the [medic-conf](https://github.com/medic/medic-conf) command line configurer tool to convert them to XForm format. The instructions below assume knowledge of XLSForm.

- A XLSForm form definition, converted to the XForm (optional) 
- A XML form definition using the ODK XForm format
- Meta information in the `{form_name}.properties.json` file (optional)
- Media files in the `{form_name}-media` directory (optional)

### Structuring a form
A typical Task form starts with an `inputs` group which contains prepopulated fields that may be needed during the completion of the form (eg patient's name, prior information), and ends with a summary group (eg `group_summary`, or `group_review`) where important information is shown to the user before they submit the form. In between these two is the form flow, usually a collection of questions grouped into pages. All data fields submitted with a form are stored, but often important information that will need to be accessed from the form is brought to the top level. Since all forms in Medic Mobile are submitted about a person or place you must make sure at least on of `place_id`, `patient_id`, and `patient_uuid` are stored at the top level.

| **type** | **name** | **label** | **relevant** | **appearance** | ... |
|---|---|---|---|---|---|
| begin group | inputs | Inputs | ./source = 'user' | field-list |
| string | source | Source |  | hidden |
| string | source_id | Source ID |  | hidden |
| end group| | |  |  |
| string | patient_id | Patient ID |  | db-object |
| string | patient_name | Patient Name |  | hidden |
| string | edd | EDD |  | hidden |
| ...
| begin group | group_review | Review |  | field-list summary |
| note | r_patient_info | \*\*${patient_name}\*\* ID: ${r_patient_id} |  |  |
| note | r_followup | Follow Up \<i class="fa fa-flag"\>\</i\> |  |  |
| note | r_followup_note | ${r_followup_instructions} |  |  |
| end group| | |  |  |

#### Inputs

#### Outputs
All forms in Medic Mobile are submitted about a person or place. In order for a submitted report to be handled properly by Medic Mobile it must have at least one of the following identifiers at the top level of the data model: `place_id`, `patient_id`, `patient_uuid`.

#### Summary page <!-- TODO -->
##### Structure
##### Styling

### Showing a form <!-- TODO -->
#### On History/Reports
#### On Profiles (see Profile section for how to show)
### Getting data into a form <!-- TODO -->
#### From Profiles
##### Inputs
##### Contact-summary (see Profile section)
#### From Tasks
##### Inputs
##### Best practices
##### source_id
#### From a database object
### Uploading forms <!-- TODO -->
#### CLI
#### UI
### Other Medic specific XForm conventions
#### Dropdown with people/places <!-- TODO -->
#### Hiding fields/groups in Reports view <!-- TODO -->
Use the `attributes::tag` with `hidden` in XLSForm
#### Creating additional docs
In version 2.13.0 and higher, you can configure your app forms to generate additional docs upon submission. You can create one or more docs using variations on the configuration described below. One case where this can be used is to register a newborn from a delivery report, as shown below. First, here is an overview of what you can do and how the configuration should look in XML:

##### Extra docs
- Extra docs can be added by defining structures in the model with the attribute db-doc="true". **Note that you must have lower-case `true` in your XLSform, even though Excel will default to `TRUE`.**

###### Example Form Model

```
<data>
  <root_prop_1>val A</root_prop_1>
  <other_doc db-doc="true">
    <type>whatever</type>
    <other_prop>val B</other_prop>
  </other_doc>
</data>
```

###### Resulting docs

Report (as before):

```
{
  _id: '...',
  _rev: '...',
  type: 'report',
  _attachments: { xml: ... ],
  fields: {
    root_prop_1: 'val A',
  }
}
```

Other doc:
```
{
  _id: '...',
  _rev: '...',
  type: 'whatever',
  other_prop: 'val B',
}
```

##### Linked docs

- Linked docs can be referred to using the doc-ref attribute, with an xpath. This can be done at any point in the model, e.g.:

###### Example Form Model
```
<sickness>
  <sufferer db-doc-ref="/sickness/new">
  <new db-doc="true">
    <type>person</type>
    <name>Gómez</name>
    <original_report db-doc-ref="/sickness"/>
  </new>
</sickness>
```

###### Resulting docs

Report:
```
{
  _id: 'abc-123',
  _rev: '...',
  type: 'report',
  _attachments: { xml: ... ],
  fields: {
    sufferer: 'def-456',
  }
}
```

Other doc:
```
{
  _id: 'def-456',
  _rev: '...',
  type: 'person',
  name: 'Gómez',
  original_report: 'abc-123',
}
```

##### Repeated docs

- Can have references to other docs, including the parent
- These currently cannot be linked from other docs, as no provision is made for indexing these docs

###### Example Form
```
<thing>
  <name>Ab</name>
  <related db-doc="true">
    <type>relative</type>
    <name>Bo</name>
    <parent db-doc-ref="/thing"/>
  </related>
  <related db-doc="true">
    <type>relative</type>
    <name>Ca</name>
    <parent db-doc-ref="/thing"/>
  </related>
</artist>
```

###### Resulting docs

Report:
```
{
  _id: 'abc-123',
  _rev: '...',
  type: 'report',
  _attachments: { xml: ... ],
  fields: {
    name: 'Ab',
  }
}
```

Other docs:
```
{
  _id: '...',
  _rev: '...',
  type: 'relative',
  name: 'Bo',
  parent: 'abc-123',
}
{
  _id: '...',
  _rev: '...',
  type: 'relative',
  name: 'Ch',
  parent: 'abc-123',
}
```

##### Linked docs example
This example shows how you would register a single newborn from a delivery report.

First, the relevant section of the delivery report XLSForm file:
![Delivery report](../img/linked_docs_xlsform.png)

Here is the corresponding portion of XML generated after converting the form:
```
<repeat>
  <child_repeat db-doc="true" jr:template="">
    <child_name/>
    <child_gender/>
    <child_doc db-doc-ref=" /delivery/repeat/child_repeat "/>
    <created_by_doc db-doc-ref="/delivery"/>
    <name/>
    <sex/>
    <date_of_birth/>
    <parent>
      <_id/>
      <parent>
        <_id/>
        <parent>
          <_id/>
        </parent>
      </parent>
    </parent>
    <type>person</type>
  </child_repeat>
</repeat>
```

If you've done your configuration correctly, all you should see when you click on the submitted report from the Reports tab is the `child_doc` field with an `_id` that corresponds to the linked doc. In this case, you could look for that `_id` on the People tab or in the DB itself to confirm that the resulting doc looks correct.

##### Repeated docs example
This example extends the above example to show how you would register one or multiple newborns from a delivery report. This allows you to handle multiple births.

First, the relevant section of the delivery report XLSForm file:
![Delivery report](../img/repeated_docs_xlsform.png)

Here is the corresponding portion of XML generated after converting the form:
```
<child_doc db-doc-ref=" /postnatal_care/child "/>
<child db-doc="true">
  <created_by_doc db-doc-ref="/postnatal_care"/>
  <name/>
  <sex/>
  <date_of_birth/>
  <parent>
    <_id/>
    <parent>
      <_id/>
      <parent>
        <_id/>
      </parent>
    </parent>
  </parent>
  <type>person</type>
</child>
```

If you've done your configuration correctly, all you should see when you click on the submitted report from the Reports tab is the `child_doc` field with an `_id` that corresponds to the first doc that was created. The other docs will have a link to the report that created them but the report will not link directly to them. Again, you could look for that `_id` on the People tab or in the DB itself to confirm that the resulting docs look correct.

#### Accessing contact-summary data
xforms have the ability to access the output of the [configured contact-summary script](https://github.com/medic/medic-docs/blob/master/configuration/contact-summary.md). This means you can have different fields, state, or information based on any known information about the contact.

To configure this, add a new instance with the id "contact-summary" to your xform somewhere below your primary instance, then bind values where you need them. Note that medic-configurer automatically adds this instance to every form so you shouldn't need to do this manually. Example:

```xml
<h:html>
  <h:head>
    <model>
      <instance>
        <visit>
          <age/>
        </visit>
      </instance>
      <instance id="contact-summary"/>
      <bind calculate="instance('contact-summary')/context/age" nodeset="/visit/age" type="string"/>
    </model>
  </h:head>
  <h:body>
    <input ref="/visit/age" />
  </h:body>
</h:html>
```

As long as you have this new instance, you can then use XPath to access all values returned in `result.context`. This works without declaring in the instance which fields are needed, so it is a very flexible solution and easier to manage when building forms.

For example, a form field with `instance('contact-summary')/context/lineage[2]/name` as a calculation will get `lineage[2].name` from a contact-summary with the following code included in `contact-summary.js`:

```
...
context.lineage = lineage;
var result = {
  fields: fields,
  cards: cards,
  context: context
};
return result;
```

Note that you can pass a large object to the form, which can then read any value, but doing so does noticeably slow the loading of the form. Because of this it is preferable to remove from the context any fields that are not being used. It is a good idea to future proof by maintaining the same structure so that fields can be added without needing to modify existing form calculations.
#### Showing fields in Reports tab <!-- TODO -->
### Tips & Tricks <!-- TODO -->
### Troubleshooting <!-- TODO -->
------------------------------------
## Collect Forms
------------------------------------
## Profiles
### Overview
### Info card
### Condition cards
### History
### Tasks
### Actions
#### Context
#### Passing data 
------------------------------------
## Tasks <!-- TODO: Already rewritten, needs review and updated screenshots -->
_Tasks guide health workers through their days and weeks. Each generated task prompts a preconfigured workflow, ensuring that the right actions are taken for the people at the right time._

_Tasks can be configured for any user of type "restricted to their place". When configuring tasks, you have access to all the contacts (people and places) that the logged in user can view, along with all the reports about them. Tasks can also pull in fields from the reports that trigger them and pass these fields in as inputs to the form that opens when you click on the task. For example, if you register a pregnancy and include the LMP, this generates follow-up tasks for ANC visits. When you click on an ANC visit task, it will open the ANC visit form and this form could "know" the LMP of the woman. In this section we will discuss how to configure such tasks._

A rules engine is used to generate the tasks using the data available in the client app. The data, comprised of docs for people, places, and the reports about them, are processed by rules engine code to emit tasks like this one:

![Task description](../img/task_with_description.png)

The rules engine code is completely configurable in `rules.nools.js`. It iterates through an object with all contacts accompanied by their reports. When the code identifies a condition that needs tasks, it generates a series of tasks based on templates in `tasks.json`. The tasks emitted by the rules engine code are then handled by the app. The app automatically shows the tasks in the Tasks tab and on contact's profiles, and removes them when they are completed.

### Configuration: `rules.nools.js`
The rules engine code receives an object containing the following:
- `contact`: the contact's doc. All contacts have `type` of either `person` or `place`.
- `reports`: an array of all the reports submitted about the contact.

The basic structure of the rules engine code is as follows:

```js
define Contact {
  contact: null,
  reports: null
}

rule GenerateEvents {
  when {
    c: Contact
  }
  then {
    if (c.contact && c.contact.type === 'person') {
      // Check for condition in person's doc
        // Create + emit task based on person's fields

      c.reports.forEach(
        function(report) {
          switch(report.form) {
            case 'form_id':
              // Check for condition in report
                // Create + emit task based on report fields
            // ...
          }
        }
      );
    }
    emit('_complete', { _id: true });
  }
}
```

To generate tasks the rules engine code must emit an object with the following properties:

| property | description | required |
|---|---|---|
|`_id`| Unique identifier for the task. Emitting another task with the same `_id` will overwrite the previous one. Generally `_id` includes the source report's ID and the event's ID in order to be unique. | yes |
| `deleted` | Expression to determine if the source docs for this task are deleted. If they are deleted the task itself can be deleted. | no |
| `doc` | Set to the contact you passed in and includes their contact info and an array of the reports about that contact | no |
| `contact` | Set to the contact you passed in. Has contact information only. | no |
| `icon` | Set to the `icon` specified for the task in `tasks.json`. | no |
| `priority` | Set to `high` priority if there is a description for the task in `tasks.json`. High priority means that the task displays a high risk icon. | no |
| `priorityLabel` | Set to the `description` listed in `tasks.json` for the task if there is a description. Use a translation key for internationalisation support. | yes |
| `date` | This is the due date of the task. It is left null during task creation and set later. | yes |
| `title` | Set to the `title` that you indicated in your `tasks.json` file. The title is the text that appears in the UI on the task. Use a translation key for internationalisation support. | yes |
| `fields` | Fields are pieces of data that display on the task summary screen. List a label and value for each field you want to display on the summary screen. | no |
| `resolved` | This tracks whether or not the task has been completed. It is set to false initially and then updated to a condition later. | yes |
| `actions` | This is an array of the actions (forms) that a user can access after clicking on a task. If you put multiple forms here, then the user will see a task summary screen where they can select which action they would like to complete. Within your array of `actions` there are some additional properties that you can define. | yes |
| `actions[n].type` | Type of action, usually `'report'`. | yes |
| `actions[n].form` | The form that should open when you click on the action. | yes |
| `actions[n].label`|  The label that should appear on the button to start this action on the task summary page ('Click here to begin the follow up' in our example summary screen above). | no |
| `actions[n].content`|  Contains fields that you want to pass into the form that will open when you click on the task or action. | no |

To separate the task structure from the logic, we have a template for each task in `tasks.json`. This file is structured as an array of task schedule objects, each with a `event` which contains one or more task templates. For each event we define the relative due date, task window, icon and title.

```json
[
  {
    "name": "task-schedule-name",
    "events": [
      {
        "id": "task-id",
        "days": 7,
        "start": 0,
        "end": 6,
        "icon": "pregnancy-1",
        "title": [
          {
            "content": "Title",
            "locale": "en"
          }
        ],
        "description": [
          {
            "content": "High risk message",
            "locale": "en"
          }
        ]
      }
    ]
  }
]
```

The individual fields are described in table below:

| field | description |
|----|----|
| `name`| This is the name of the task schedule. It's used when retrieving a particular task schedule from `tasks.json` for use in `rules.nools.js`.|
| `events`| These are the individual tasks in the schedule. You may have one or more tasks in your schedule. For each event, you need to include the following |
| `events[n].id` | This is an `id` you define for each of your tasks.|
| `events[n].days` | Due date for the task. It is the number of days after the schedule start date that a task is due.|
| `events[n].start` | The number of days before the task due date that the task should appear in the task list.|
| `events[n].end` | The number of days after the task due date that the task should continue to appear in the task list.|
| `events[n].icon` | You can use any icon that you like, but make sure the icon has been uploaded to your instance and the name matches.|
| `events[n].title` | The name of your task that will appear to the user. This field supports locales, so you can include translations if you have users viewing the app in different languages on the same instance.|
| `events[n].description` | This is optional. It is a second line of text that can appear at the right side of the task on the tasks list.|

To initialize a task we use a `createTask` function, passing to it the contact the task is about, the specific `event` from the task schedule, and the `report` that triggered the task:
```js
    var createTask = function(contact, event, report) {
      return new Task({
        _id: report._id + '-' + event.id,
        deleted: (contact.contact ? contact.contact.deleted : false) || (report ? report.deleted : false),
        doc: contact,
        contact: contact.contact,
        icon: event.icon,
        priority: event.description ? 'high' : null,
        priorityLabel: event.description ? event.description : '',
        date: null,
        title: event.title,
        resolved: false,
        actions: []
      });
    };

```
The newly initialized task needs to be manipulated a bit more before it is ready to be emitted. Typically, the fields that need to be set after initialization are the actual `date` the task is due, the possible `actions` with data to be passed to forms, and the `resolved` condition. Additionally, based on the specific task, it is possible that the `_id` needs to be modified further to be unique, and that the `priority` and `priorityLabel` need to be calculated dynamically.

In order for a task to show for an appropriate number of days before and after the due date we only emit tasks when the current time is between the start and end days from the due date. To make this easier, we use the `emitTasks` function to only emit the task between the `start` and `end` days for the task, as specified in the task template.

```js
    var emitTask = function(task, scheduleEvent) {
      if (Utils.isTimely(task.date, scheduleEvent)) {
        emit('task', task);
      }
    };
```

Putting these concepts all together, here is an example snippet where a task is created, modified, then emitted for each event in a task schedule.
```js
var schedule = Utils.getSchedule('pregnancy-missing-visit');
if (schedule) {
  for (var k = 0; k < schedule.events.length; k++) {
    var event = schedule.events[k];
    var dueDate = new Date(Utils.addDate(new Date(report.scheduled_tasks[i].due), event.days));
    var task = createTask(contact, event, report);
    // each group needs its own task, otherwise will be combined into one
    task._id += '-' + i;
    task.date = dueDate;
    task.priority = isHighRiskPregnancy ? 'high' : null;
    task.priorityLabel = isHighRiskPregnancy ? ( schedule.description ? schedule.description : 'High Risk' ) : '';
    task.actions.push({
        type: 'report',
        form: 'pregnancy_visit',
        label: 'Follow up',
        content: {
        source: 'task',
        source_id: report._id,
        contact: contact.contact
        }
    });
    // Resolved if there is a newer pregnancy, there has been a delivery, or visit received in window
    task.resolved = report.reported_date < newestPregnancyTimestamp
        || report.reported_date < newestDeliveryTimestamp
        || isFormFromArraySubmittedInWindow(c.reports, antenatalForms, Utils.addDate(dueDate, event.start * -1).getTime(), Utils.addDate(dueDate, event.end + 1).getTime());

    emitTask(task, event);
  }
}
```

#### Utils
Some utility functions are available to your rule configuration and have been included to make common tasks much easier. To use the function call `Utils.<function-name>(<params>)`, for example `Utils.addDate(report.reported_date, 10)`.

| Name | Description |
|---|---|
| isTimely(date, event) | Returns true if the given date is after the start date and before the end date of the event. |
| addDate(date, days) | Returns a new Date set to midnight the given number of days after the given date. If no date is given the date defaults to today. |
| getLmpDate(doc) | Attempts to work out the LMP from the given doc. If no LMP is given it defaults to four weeks before the reported_date. |
| getSchedule(name) | Returns the task schedule with the given name from the configuration. |
| getMostRecentTimestamp(reports, form) | Returns the reported_date of the most recent of the reports with form ID matching the given form. |
| getMostRecentReport(reports, form) | Like `getMostRecentTimestamp` but returns the report, not just the reported_date. |
| isFormSubmittedInWindow(reports, form, start, end) | Returns true if any of the given reports are for the given form and were reported after start and before end. |
| isFirstReportNewer(firstReport, secondReport) | Returns true if the firstReport was reported before the secondReport. |
| isDateValid(date) | Returns true if the given date is a validate JavaScript Date. |
| now() | Returns the current Date. |
| MS_IN_DAY | A constant for the number of milliseconds in a day. |

If you can think of any others you'd like to be included raise an issue in [medic/medic-webapp](https://github.com/medic/medic-webapp/issues).

### Uploading <!-- TODO -->
### Examples
All of the following examples show code that runs for each report of a certain type.

##### ICCM Follow-up
In this example, we are generating a follow-up for either a treatment or a referral, depending on the outcome of the ICCM assessment.

```javascript
case 'assessment':
  var followupType = 'treat'; // will be one of: treat, refer

  if (r.fields) {
    // The follow-up schedule is based on the `reported_date`, so store it for use later
    var reportedDate = new Date(r.reported_date);
    // Set schedule name to the one for treatment follow-up
    var scheduleName = 'assessment-treatment';

    // Check to see if the patient was referred
    if (r.fields.referral_follow_up == 'true') {
      // If they were, change the follow-up type and schedule name accordingly
      followupType = 'refer';
      scheduleName = 'assessment-referral';
    }

    // Get the task schedule that you specified in `tasks.json`
    var schedule = Utils.getSchedule(scheduleName);

    if (schedule) {
      schedule.events.forEach(function(s) {
        // Determine the due date by taking the base date (`reported_date` in this case) and adding the number of days specified
        var dueDate = new Date(Utils.addDate(reportedDate, s.days));
        var visit = createTask(c, s, r);
        // Set the due date of the task
        visit.date = dueDate;
        // This task should be cleared if the `assessment_follow_up` form is submitted within the task window
        visit.resolved = Utils.isFormSubmittedInWindow(c.reports, 'assessment_follow_up', Utils.addDate(dueDate, s.start * -1).getTime(), Utils.addDate(dueDate, s.end).getTime() );
        // We only have one available action this time
        visit.actions.push({
          type: 'report',
          form: 'assessment_follow_up',
          content: {
            source: 'task',
            source_id: r._id,
            contact: c.contact,
            // Include the follow-up type as an input to the `assessment_follow_up` form
            t_follow_up_type: followupType,
          }
        });
        emitTask(visit, s);
      });
    }
  }
  break;
```

##### Pregnancy Visits
In this example, we see how we can use the task summary screen and have two available actions from one task.

```javascript
case 'pregnancy':

  if ( !(r.fields && r.fields.lmp_date ) ) { break; }

  // The schedule will be based on the LMP date, so store it
  var lmp = new Date(r.fields.lmp_date);

  // Set the schedule name
  var scheduleName = 'pregnancy-healthy';
  // If the pregnancy is is high-risk, adjust the schedule name
  if ((pregnancy.fields.risk_factors && pregnancy.fields.risk_factors != '') 
    || (pregnancy.fields.danger_signs && pregnancy.fields.danger_signs != '')
    || parseInt(pregnancy.fields.patient_age_at_lmp, 10) < 18
    || parseInt(pregnancy.fields.patient_age_at_lmp, 10) > 35 ){
      scheduleName = 'pregnancy-high-risk';
  }

  // Get the specified task schedule
  var schedule = Utils.getSchedule(scheduleName);
  if (schedule) {
    schedule.events.forEach(function(s) {
      // Determine the due date by taking the base date (`lmp`) and adding the number of days you specified
      var dueDate = new Date(Utils.addDate(lmp, s.days));
      var visit = createTask(c, s, r);
      // Set the task due date
      visit.date = dueDate;
      // Add fields to be displayed on the task summary screen
      visit.fields.push({
        label: [
          {
            content: 'Patient Age',
            locale: 'en'
          }
        ],
        value: [
          {
            content: age,
          }
        ]
      },
      {
        label: [
          {
            content: 'EDD',
            locale: 'en'
          }
        ],
        value: [
          {
            content: edd_date,
          }
        ]
      });
      // This task should be cleared if there is a newer pregnancy, there has been a delivery, or visit done in the task window
      visit.resolved = r.reported_date < newestPregnancyTimestamp || r.reported_date < newestPostnatalTimestamp || Utils.isFormSubmittedInWindow(c.reports, 'pregnancy_visit', Utils.addDate(dueDate, s.start * -1).getTime(), Utils.addDate(dueDate, s.end).getTime());
      // We are adding two possible actions, Pregnancy Visit and Delivery Report
      visit.actions.push({
        type: 'report',
        form: 'pregnancy_visit',
        label: 'Pregnancy Visit',
        content: {
          source: 'task',
          source_id: r._id,
          contact: c.contact,
          // Include the LMP so that we can use it during the pregnancy visit
          t_lmp_date: lmp.toISOString()
        }
      },
      {
        type: 'report',
        form: 'delivery_report',
        label: 'Delivery Report',
        content: {
          source: 'task',
          source_id: r._id,
          contact: c.contact,
          // Include the LMP so that we can use it during the pregnancy visit
          t_lmp_date: lmp.toISOString()
        }
      });
      emitTask(visit, s);
    });
  }
```

### Tips & Tricks
1. `actions[n].content` is where you can pass form fields from the report that triggered the action to the form that will open when you click on a task. Be sure you include `content.source: 'task'`, `content.source_id: r._id` and `content.contact: c.contact`. The `source` and `source_id` are used in Analytics to relate a task to the action that triggered it.
1. There are some use cases where information collected during an action within a task schedule may mean that the task schedule must change. For example, if you register a child for malnutrition follow-ups, you collect the height and weight during registration and tasks for follow-ups are created based on the registration. At the next visit (first follow-up), you collect the height and weight again and you want to update these so that future tasks reference this new height and weight. You can either clear and regenerate the schedule after each follow-up visit is done, or you can create only one follow-up at a time so that height and weight are always referencing the most recent visit.
1. Given the way that the rules engine works, code that generates tasks must be immutable. Otherwise you will find that tasks are not clearing properly.
1. If you have more than one action, click a prompted task will show a summary screen with fields you have passed along with a button for each possible action.
![Task summary screen](../img/task_summary_screen.png)
1. If you have a single action for a task, click the task will bring you straight to the specified form.
![Task form](../img/task_form.png)


### Troubleshooting
1. Cannot see tasks: Makes sure your user is an offline user
1. Tasks is not clearing: Make sure the the code that generates the task is immutable.

------------------------------------
## Targets <!-- TODO: Marc to revise to similar structure as Tasks -->
Targets refers to our in-app analytics widgets. These widgets can be configured to track metrics for an individual CHW or for an entire health facility, depending on what data the logged in user has access to. Targets can be configured for any user that has offline access (user type is "restricted to their place"). When configuring targets, you have access to all the contacts (people and places) that your logged in user can view, along with all the reports about them.

Targets are configured in two places:
- `targets.json` is where you define how the target looks, including the title, icon and goal (if applicable). It is also where you set the `context` to decide who should see the target.
- `rules.nools.js` is where you define the calculation for each of your targets.

### Template: `targets.json`
Each of your targets must be defined so that the app knows how to render it. You will need to include the following properties for each of your targets:

* `type`: There are currently two types of targets, `count` and `percent`. These are illustrated above in the Types of Widgets section. 1 & 2 are the `count` type and 3 is the `percent` type.
* `id`: This can be whatever you like, but it must match the `type` property of the target being emitted in `rules.nools.js`.
* `icon`: You can use any icon that you like, but make sure the icon has been uploaded to your instance and the name matches.
* `goal`: For percentage targets, you must put a positive number. For count targets, put a positive number if there is a goal. If there is no goal, put -1.
* `context`: This is an expression similar to form context that describes which users will see a certain target. In this case, you only have access to the `user` (person logged in) and not to the `contact` since you are not on a person or place profile page.
* `translation_key`: The name of the translation key to use for the title of this target.
* `subtitle_translation_key`: The name of the translation key to use for the subtitle of this target. If none supplied the subtitle will be blank.
* `percentage_count_translation_key`: The name of the translation key to use for the percentage value detail shown at the bottom of the target, eg: "(5 of 6 deliveries)". The translation context has `pass` and `total` variables available. If none supplied this defaults to "targets.count.default".

#### Plain count with no goal

![Count no goal](../img/target_count_no_goal.png)

#### Count with a goal

![Count with goal](../img/target_count_with_goal.png)

#### Percentage with no goal

![Percentage no goal](../img/target_percent_no_goal.png)

#### Percentage with a goal

![Percentage with goal](../img/target_percent_with_goal.png)

#### Example Target Definition - Count

```JSON
{
  "type": "count",
  "id": "assessments-u1",
  "icon": "infant",
  "goal": 4,
  "context": "user.parent.parent.name == 'San Francisco'",
  "translation_key": "targets.assessments.title",
  "subtitle_translation_key": "targets.assessments.subtitle"
}
```

#### Example Target Definition - Percent

```JSON
{
  "type": "percent",
  "id": "newborn-visit-48hr",
  "icon": "mother-child",
  "goal": 85,
  "translation_key": "targets.visits.title",
  "subtitle_translation_key": "targets.visits.subtitle",
  "percentage_count_translation_key": "targets.visits.detail"
}
```

### Creation: `rules.nools.js`
A rules engine processes all contacts and reports and emits data to the defined targets. The rules engine is configured in `rules-nools.js` by preparing the target instances, and then emitting them. Below are some helpful functions, and examples from the most basic to the more complex.

#### Creating a Target

Here is a sample function to create a data point for a target, called a target instance.

```javascript
var createTargetInstance = function(type, report, pass) {
  return new Target({
    _id: report._id + '-' + type,
    deleted: !!report.deleted,
    type: type,
    pass: pass,
    date: report.reported_date
  });
};
```

When creating a target, you are required to pass in a type, a report and pass (as shown in the above function). Targets have several properties:

* `_id`: By default, the `_id` is set to [report ID]-[type]. [report ID] is the `_id` of the report that you passed in.
* `deleted`: Set based on whether the report that generated the target is deleted.
* `type`: Set to the passed in value that you provide. The `type` must match the `id` that you list in your `targets.json` file. More on the `targets.json` file below.
* `pass`: Can be true or false. True if the report meets the specified condition and false if the report doesn't meet the condition. The total number of target emissions is always equal to the number of targets emitted with `pass: true` plus the number of targets emitted with `pass: false`.
* `date`: By default, this is set to the `reported_date` of the report that you provided.

It's possible to change any of the properties of a target before you emit it. This can come in handy when configuring different types of targets. Some examples will be outlined later in this document. Once you have created your target and made any changes to its properties, make sure you emit the target using the `emitTargetInstance` function.

#### Emitting a Target

```javascript
var emitTargetInstance = function(instance) {
  emit('target', instance);
};
```

#### Simple Count - This Month

The most basic target is a simple count of a particular type of report. In this case, we are counting the number of pregnancy registrations.

```javascript
if (c.contact != null) {
  if(c.contact.type === 'person'){
    c.reports.forEach(function(r) {
      if (r.form === 'pregnancy') {
        // Finds instances of the pregnancy registration form. No conditions, just counts every pregnancy form submission.
        var instance = createTargetInstance('pregnancy-registrations', r, true);
        emitTargetInstance(instance);
      }
    });
  }
}
```

You may also want to count the number of households or people registered. This target counts up the number of `clinic`s, in this case households, that have been registered. Using this target will give you a count of families registered this month.

```javascript
if (c.contact != null) {
  if(c.contact.type === 'clinic'){
    // Find all households
    // NO condition to check the form name since place forms are not submitted as reports
    var instance = createTargetInstance('hh-registration', c.contact, true);
    emitTargetInstance(instance);    
  }
}
```

#### Simple Count - All Time

You may also want to count the total number of pregnancies registered over all time. The key to all-time targets is adjusting the target date to sometime in the current month. The easiest way is to set the target's date to today.

```javascript
if (c.contact != null && c.contact.type === 'person') {
  c.reports.forEach(function(r) {
    var today = new Date();

    if (r.form === 'pregnancy') {
      // Find instances of the pregnancy registration form.
      var instance = createTargetInstance('pregnancy-registrations', r, true);
      // Set the target's date to today's date
      instance.date = now.getTime();
      emitTargetInstance(instance);
    }
  });
}
```

You can do the same with all-time household registrations. Simply set the target's date to today's date to get an all-time count.

```javascript
if (c.contact != null) {
  var today = new Date();

  if(c.contact.type === 'clinic') {
    // Find all households
    var instance = createTargetInstance('hh-registration', c.contact, true);
    // Set the target's date to today's date
    instance.date = today.getTime();
    emitTargetInstance(instance);
  }
}
```

#### Count with Conditions - This Month

Sometimes you may want to count a subset of a particular type of form that meets certain conditions. This example looks for ICCM assessments where the diagnosis was malaria and will give us the total this month.

```javascript
if (c.contact != null && c.contact.type === 'person') {
  c.reports.forEach(function(r) {
    // Find all assessment forms where the CHW was instructed to treat for malaria.
    if (r.form === 'assessment' && r.fields.treat_for_malaria == 'true') {
	  // Create a target instance for each of these assessments where the CHW treated for malaria
      var instance = createTargetInstance('treatment-malaria', r, true);
      emitTargetInstance(instance);
    }
  });
}
```

#### Count with Conditions - All Time

If you want to count a subset of a particular form that meets certain conditions over all time, simply set the target's date to today's date, as shown above.

```javascript
if (c.contact != null && c.contact.type === 'person') {
  c.reports.forEach(function(r) {
    var today = new Date();
    var dob_1yr = new Date();
    dob_1yr.setFullYear(today.getFullYear()-1);

    // Find all assessment forms where a child under 1 year was assessed
    if (r.form === 'assessment' && dob_contact > dob_1yr) {
      var instance = createTargetInstance('assessments-u1', r, true);
      // Set the target's date to today's date
      instance.date = today.getTime();
      emitTargetInstance(instance);
    }
  });
}
```

#### Percent - This Month

Percent targets always have a condition, so you will be emitting some targets that have `pass: true` and some that have `pass: false`. This is achieved by setting a variable, `pass`, equal to an expression that evaluates to either true or false. When calculating the percentage, it will be number of true targets divided by number of true targets plus number of false targets.

```javascript
// % Newborn Care Visit within 48 hours
if (c.contact != null && c.contact.type === 'person') {
  c.reports.forEach(function(r) {
    var today = new Date();
    // Find all delivery reports
    if (r.form === 'postnatal_care' && r.fields.delivery_date != '') {
      // Calculate the 48 hour cutoff (2 days after the delivery date at 23:59)
      var followup_cutoff = new Date(r.fields.delivery_date);
      followup_cutoff.setDate(followup_cutoff.getDate() + 2);
      followup_cutoff.setHours(23, 59, 59);
      // See if the date the delivery report was submitted is before the 48 hour cutoff
      var pass = new Date(r.reported_date) <= followup_cutoff;
      // Pass in the pass variable when creating the target instead of true or false
      var instance = createTargetInstance('newborn-visit-48hr', r, pass);
      emitTargetInstance(instance);
    }
  });
}
```

#### Percent - All-time

This target finds all delivery reports and checks to see if the delivery was at the health facility. It sets the target's date to today's date so that we can count over all time.

```javascript
// % DELIVERIES AT HEALTH FACILITY ALL-TIME
if (c.contact != null && c.contact.type === 'person') {
  var today = new Date();
  // Calculate most recent delivery timestamp for the current contact
  var newestDeliveryTimestamp = Math.max(
            Utils.getMostRecentTimestamp(c.reports, 'D'),
            Utils.getMostRecentTimestamp(c.reports, 'delivery')
            );

  c.reports.forEach(function(r) {
    // Find all delivery reports
    if (r.reported_date === newestDeliveryTimestamp && (r.form === 'D' || r.form === 'delivery')) {
      // If the delivery was in a facility, pass = true; if not, pass = false
      var pass = r.fields.delivery_code && r.fields.delivery_code.toUpperCase() == 'F';
      // Pass in the variable pass when creating the target
      var instance = createTargetInstance('delivery-at-facility-total', r, pass);
      instance.date = today.getTime();
      emitTargetInstance(instance);
    }
  });
}
```

### Uploading <!-- TODO -->
### Examples
This section contains some other examples of more complex targets.
#### Calculate Percent of Households that were Surveyed - All-Time

In this case, we are emitting a false target for every household and then a true target for every household for which a survey was done. Because the true target will be emitted after the false target, it will overwrite the false target.

```javascript
// Find all households
if(c.contact.type === 'clinic'){
  var today = new Date();
  // Find the time of the most recent survey
  var newestEquitySurveyTimestamp = Utils.getMostRecentTimestamp(c.reports, 'family_equity');

  // Emit a false target for every household that has been registered to make sure that we capture every household
  var instance = createTargetInstance('surveys-conducted', c.contact, false);
  instance.date = today.getTime();
  emitTargetInstance(instance);

  // Review all reports for the current household
  c.reports.forEach(function(r) {
    // Find out if a survey form was completed for this household
    if (r.form === 'family_equity' && r.reported_date >= newestEquitySurveyTimestamp){
      // If there is a survey, emit a true target for the household to replace the false target
      // This will result in displaying the % of households registered that had a survey done
      var instance = createTargetInstance('surveys-conducted', c.contact, true);
      // Set the target's date to today to get an all-time count
      instance.date = today.getTime();
      emitTargetInstance(instance);
    }
  });
}
```

#### Count Number of Households Visited by CHW - This Month

```javascript
if (c.contact != null && c.contact.type === 'person') {
  // For each report about a family member
  c.reports.forEach(function(r) {
    // Create a true target that refers to the household the person belongs to
    var instance = createTargetInstance('hh-visits', c.contact.parent, true);
    // Set the target date to the current report
    instance.date = r.reported_date;
    // If the current report was submitted this month, emit the target
    if(r.reported_date >= month_start_date) {
      emitTargetInstance(instance);
    }
  });
}
```

#### Calculate Percent of CHWs Visited by their Manager - This Month

This target is for a CHW manager. It calculates the percentage of the CHWs they manage that they have visited this month.

```javascript
// health_center is a CHW area in this case
if (c.contact != null && c.contact.type === 'health_center'){
  var newestCHWVisitTimestamp = Utils.getMostRecentTimestamp(c.reports, 'chw_visit');

  // Look for all CHW areas for which you are the supervisor
  if(c.contact.supervisor == user._id) {
    // Create a false target for each CHW area
    // Note that we are using the contact to create the target
    var instance = createTargetInstance('chws-visited', c.contact, false);
    // Set the target date to today so that we have a false target this month for every CHW area
    instance.date = today.getTime();
    emitTargetInstance(instance);
  }
  c.reports.forEach(function(r) { 
    // Find all of the CHW visit forms that are the most recent and that are for CHWs you supervise
    if(r.form == 'chw_visit' && r.reported_date >= newestCHWVisitTimestamp && c.contact.supervisor == user._id) {
      // If a CHW visit was done, emit a true target
      // Use the contact to create the target so that it matches the targets emitted above and will override them as needed
      var instance = createTargetInstance('chws-visited', c.contact, true);
      // Set the target date to the date of the CHW visit so that we only count visits done this month
      instance.date = r.reported_date;
      emitTargetInstance(instance);
    }
  });
}
```

#### Percent of PNC Visits within 72 hours of Birth - This Month

This target determines the % of PNC visits that occurred within 72 hours of birth. First, it looks at the PNC visits that were done to see if they were done on time. Second, it looks at all pregnancies registered with recent EDDs to see if a PNC visit was done. If not, it counts as a PNC visit that was not on-time.

```javascript
if (c.contact != null && c.contact.type === 'person') {
  c.reports.forEach(function(r) {
    // For each PNC form, check to see if it's a delivery report and if it is more recent than the most recent pregnancy registration
    if (r.form === 'postnatal_care' && r.fields.delivery_date != '' && r.reported_date > newestPregnancyTimestamp) {
      // Create a variable to track the cutoff date for when PNC must be done (by 3 days after delivery date at 23:59)
      var followup_cutoff = new Date(r.fields.delivery_date);
      followup_cutoff.setDate(followup_cutoff.getDate() + 3);
      followup_cutoff.setHours(23, 59, 59);
      // Pass = true if the PNC/delivery report was submitted before the cutoff
      var pass = new Date(r.reported_date) <= followup_cutoff;
      var instance = createTargetInstance('newborn-visit-72hr', r, pass);
      emitTargetInstance(instance);
    }

    // Look at each pregnancy registration to see if the EDD falls within the current month. This tells us if there are any pregnancies for which we expect a PNC/delivery report this month.
    // Make sure the pregnancy registration is the most recent registration and that it is more recent than the most recent PNC/delivery report so that there is no overlap with the previous section where we looked at PNC/delivery reports.
    if (r.form === 'pregnancy' && r.reported_date >= newestPregnancyTimestamp && r.reported_date > newestPostnatalTimestamp) {
      // We only want to look at pregnancies with EDDs this month that were at least 3 days ago
      // Create a variable to set the cutoff for EDDs we want to consider (3 days ago)
      var edd_cutoff = new Date();
      edd_cutoff.setDate(today.getDate() - 3);
      edd_cutoff.setHours(23, 59, 59);
      // Create a variable to keep track of the start date of this month
      var month_start_date = new Date(today.getFullYear(), today.getMonth(), 1);
      // Calculate the EDD based on the LMP reported in the pregnancy registration
      var edd = new Date(r.fields.lmp_date);
      edd.setDate(edd.getDate() + 280);
      edd.setHours(0,0,1);

      var pass;
      // Check to see if the EDD falls this month but before the EDD cutoff. 
      // Make sure the most recent pregnancy registration is more recent than the most recent pregnancy visit OR the most recent pregnancy visit is more recent than the most recent pregnancy registration but there has been no delivery report.
      if(edd >= month_start_date && edd <= edd_cutoff && (newestPregnancyTimestamp > newestPregnancyVisitTimestamp || (newestPregnancyVisitTimestamp > newestPregnancyTimestamp && newestPregnancyVisit.fields.discontinue_follow_up === 'false'))) {
        // Create a variable to track the start of the window for which we want to look for PNC/delivery reports for any EDDs this month
        var edd_window_start = new Date(edd);
        edd_window_start.setDate(edd.getDate() - 60);
        // If the most recent PNC/delivery report occurred within the 60-day window, pass = true because the PNC/delivery report was done
        // We are assuming that any PNC within 60 days would be for the pregnancy with an EDD this month
        if(newestPostnatalTimestamp >= edd_window_start && newestPostnatalTimestamp < today) {
          pass = true;
        }
        // If not, pass = false because the PNC/delivery report was not done but we were expecting it to have happened
        else {
          pass = false;
        }
        var instance = createTargetInstance('newborn-visit-72hr', r, pass);
        // Set the target date to the EDD since we know that the EDD will be within the current month
        instance.date = edd;
        emitTargetInstance(instance);
      }
    }
  });
}
```

### Tips & Tricks
1. Percentage targets are always equal to: `(number of true targets) / (number of true targets + number of false targets)`
1. It's possible to emit a target that refers to the same form or contact multiple times. This can be used to calculate percentage targets by emitting a false target for each of the forms or contacts that you want to include and then emitting true only for the ones that meet certain conditions. See the Calculate Percent of Households that were Surveyed example below.
1. Remember that targets are emitted in a specific order, so if you are using the method in the previous tip, this might impact your results. The app will always use the target emitted most recently, so if you emit false, true, false for the same form or contact, then the app will consider it a false target, even though there was a true emitted at some point. 

### Troubleshooting
------------------------------------
------------------------------------
# Set-up
## Contacts
### Create [via UI, needs training module]
### Edit [via UI, needs training module]
### Bulk create
## Users 
### Overview
### Create [via UI, needs training module] <!-- TODO: Jill -->
### Bulk Creation (conf#61)
### Permissions <!-- TODO: Derick -->
#### Overview
#### User roles
| Role | Description |
|-----|-----|
|`district_admin`|  |

#### Reference Table
| Permission | Description |
|-----|-----|
|`can_blah_blah`|  |
## Data Migration
------------------------------------
------------------------------------
# Deploy + Maintain
## Versioning
## Upgrades
## Release notes
## Deploying
## Local
## Development Setup
## Contributing code
## Export
------------------------------------
------------------------------------