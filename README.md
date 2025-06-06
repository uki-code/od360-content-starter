# od360-content-starter

## Integrating Content with OpenDash 360

Content integrates with OpenDash 360 via the CMI5 standard.

## CMI5 Standard

The CMI5 specification is shepherded by AICC.

### CMI5 Overview

Here is a conceptual overview: https://aicc.github.io/CMI-5_Spec_Current/flows/cmi5-overview.html
UKI fills the "Administrator" role
Content partner fills the "Author" role
Client organization personnel fill the "Learner" role

Here is a good entry point: https://aicc.github.io/CMI-5_Spec_Current/

Full text of the spec: https://github.com/AICC/CMI-5_Spec_Current/blob/quartz/cmi5_spec.md

### CMI5 Components

CMI5 defines 3 core components:

1. Learning management system (LMS)
  * tracks assignment of training, user progress, launching content ("Assignable Units"—AUs)
  * In our case, this role is filled by OpenDash 360 (OD360)
    * Developed and managed by UKI
2. Learning Record Store (LRS)
  * records learner progress: submitted answers, in-progress AU state, completion
  * Implements XAPI
    * REST & JSON API
    * Runtime component of CMI5 is a subset of XAPI (called a "profile")
  * In our case, this role is filled by LRSQL
    * https://github.com/yetanalytics/lrsql
    * Licensed under Apache 2
    * Developed by Yet Analytics
    * Operated by UKI
3. Assignable Units (AUs)
  * Atomic unit of content in CMI5
  * Multiple AUs together comprise a "Course"
    * Course is the atomic unit of import and assignment
    * AU is the atomic unit of launch
    * Course structure is described by content provider to LMS during import
  * In our case, this role is filled by content partner
    * Each lesson/unit/lab is an AU in CMI5
  * Must be imported into LMS for use by learners
    * Import process ingests course structure in `cmi5.xml`
      * Or CMI5 package zip file, which includes `cmi5.xml` at the root
    * Example course templates are available here: https://xapi.com/cmi5/example-course-templates/
    * For browser-based content, use the CMI5 Profile library from XAPI.js
      * https://www.xapijs.dev/cmi5-profile-library/introduction
      * This library manages most of the CMI5 lifecycle for an AU provider

### CMI5 Content Lifecycle

CMI5 defines 5 core events in the learner-content lifecycle. The spec requires each event to be recorded for each AU launch. This interaction is detailed here: https://aicc.github.io/CMI-5_Spec_Current/flows/au-flow.html

### CMI5 Content Development & Validation Harness

A local CMI5 harness is available by running the reference implementation CATAPULT player, available and documented here: https://github.com/adlnet/CATAPULT/tree/main/player. The CATAPULT project is provided under the Apache License, Version 2.0. At the link given you will find a Docker Compose configuration which will allow running the CATAPULT player locally.

This component simulates the role of an LMS, into which content can be imported, and which will initiate the launch interaction with content in the same way that OpenDash 360 will.

In order to test content locally an LRS is also required. We use an Open Source LRS called LRSQL. It ships with instructions for running it locally under Docker here: https://github.com/yetanalytics/lrsql/blob/main/doc/docker.md
