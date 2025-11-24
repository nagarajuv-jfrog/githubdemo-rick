---
title: Create an Application in the Platform UI
deprecated: false
hidden: false
metadata:
  robots: index
---
You can use the platform UI to create an application for managing the SDLC of a software product developed by your organization.

As you complete the wizard, your definitions appear in the Application Details pane to the right of the wizard.

**To create an application:**

1. Select the project in which the application will reside from the dropdown list. 

   <Image align="center" border={false} width="50% " src="https://files.readme.io/295ee03a8bbcc1d477fe058ec077cc222687a80041fd6287b9c9cc2b4faa661a-831848_hpr.png" />

   <Callout icon="📘" theme="info">
     Applications must be created within the context of a specific project. You cannot create an application when working in All Projects.
   </Callout>
2. In the ​**Platform**​ module, select ​**AppTrust > Applications**​​ to display the Applications page.
3. Click **Create Application** to open the New Application Wizard.
4. In **step 1** of the wizard define application details:
   1. Enter a unique display name and key for the application. The key must contain between 2-64 lowercase alphanumeric characters and hyphens, beginning with a letter.
   2. Add an optional description of the application.
   3. Select the maturity level of this application: ​**Unspecified**​​, ​**Experimental**​​, ​**Production**​​, or ​**End of Life**
   4. In the Business Criticality field, define the impact of this application on your business: ​**Unspecified**​​, ​**Low**​​, ​**Medium**​​, ​**High**​​, or ​**Critical**
5. Click **Next** to continue.​​​​
6. In ​**step 2​​** of the wizard, optionally enter one or more key-value pairs to act as labels associated with the application. These labels can be used to help identify the application within your organization. Labels are limited to 255 characters, beginning and ending with an alphanumeric character ([a-z0-9A-Z]) with dashes (-), underscores (_), dots (.), and alphanumerics between.
7. Click **Next** to continue.
8. In **​step 3**​ of the wizard, define the owners of the application. For each owner, select the name of a user or group ​defined​ by the administrator and then click ​**Add**​​.
9. When you are finished, click **​Create Application​​**. The new application is added to the Applications table.

<br />
