![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/main/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Predictive Maintenance for remote field devices
</div>

<div class="MCWHeader2">
Whiteboard design session student guide
</div>

<div class="MCWHeader3">
May 2021
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only, and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third-party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2021 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are the property of their respective owners.

**Contents**

<!-- TOC -->

- [Predictive Maintenance for remote field devices whiteboard design session student guide](#predictive-maintenance-for-remote-field-devices-whiteboard-design-session-student-guide)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Step 1: Review the customer case study](#step-1-review-the-customer-case-study)
    - [Customer situation](#customer-situation)
      - [Telemetry data](#telemetry-data)
    - [Customer needs](#customer-needs)
    - [Customer objections](#customer-objections)
    - [Infographic for common scenarios](#infographic-for-common-scenarios)
  - [Step 2: Design a proof of concept solution](#step-2-design-a-proof-of-concept-solution)
  - [Step 3: Present the solution](#step-3-present-the-solution)
  - [Wrap-up](#wrap-up)
  - [Additional references](#additional-references)

<!-- /TOC -->

# Predictive Maintenance for remote field devices whiteboard design session student guide

## Abstract and learning objectives

In this whiteboard design session, you will work with a group to evaluate Azure's PaaS and SaaS-based IoT products and design a solution that uses the optimal combination of tools to fulfill Fabrikam's needs. You will provide guidance for designing a solution that simplifies IoT device management and reporting, enabling Fabrikam to more rapidly implement their IoT strategy without requiring a lot of custom development. Next, you will design a solution that deploys a trained predictive maintenance Machine Learning model and uses a stream processing pipeline that makes predictions with the model in near real-time. At the end of this pipeline is an alert that is sent to the oil pump maintenance team when a pump failure is imminent.

At the end of this whiteboard design session, you will be better able to design an IoT-based predictive maintenance solution in Azure.

## Step 1: Review the customer case study

**Outcome**

Analyze your customer's needs.

Timeframe: 15 minutes

Directions: With all participants in the session, the facilitator/SME presents an overview of the customer case study along with technical tips.

1.  Meet your table participants and trainer.

2.  Read all of the directions for steps 1-3 in the student guide.

3.  As a table team, review the following customer case study.

### Customer situation

Fabrikam, Inc. creates innovative IoT solutions for the oil and gas manufacturing industry. It is beginning work on a new, predictive maintenance solution that targets rod pumps (the iconic pivoting pumps that dot oil fields around the world). With their solution in place, companies will be able to monitor and configure pump settings and operations remotely, and only send personnel onsite when necessary for repair or maintenance when the solution indicates that something has gone wrong. However, Fabrikam wants to go beyond reactive alerting; they want to want to enable the solution with the ability to _predict_ problems so they can be averted before a fault occurs and damage is done.

One of Fabrikam's challenges is managing IoT devices at scale. They want to be able to securely store credentials on their devices before sending them to their customers. When the devices connect to the cloud, they want to have an approval process that activates those devices so they can start sending telemetry securely. All data in transit must be encrypted.

Another decision point for Fabrikam is whether they would benefit from a software-as-a-service (SaaS) cloud-based offering, or a more customized platform-as-a-service (PaaS) solution. Fabrikam's technical leadership believes that, since IoT is not one of their top disciplines, and because technology is rapidly changing in the IoT space, they would benefit most from a SaaS-based solution. On the other hand, they want to know what the range of IoT PaaS options there are on Azure so they can make an informed decision on which route they should invest their time and resources. Given their current lack of IoT experience, Fabrikam would like to build a proof of concept (PoC) using a SaaS product that they can quickly get started with to evaluate whether it meets their immediate and long-term needs. These needs include device management, visualization, reporting, control, and monitoring. Ideally, the solution will be highly scalable and secure, should they decide to transition from a PoC to a pilot deployment with several customers. When they do start expanding to several customers, they would like a transparent pricing structure they can use to project costs and pass those costs to their customers based on their usage.

Whichever cloud-based solution Fabrikam pursues, they want to know how they can visualize all of the data generated by sensors on each rod pump. These sensors include power output from motors, motor speed, the pump rate measured in strokes per minute, how long the pump is on, and casing friction measured in psi, to name a few. Each of these sensors output data at different rates and measurements, complicating any effort to build meaningful charts and dashboards. The information needs to be easily digested by analysts and technicians alike, with options to filter and explore the data over a timeline and within groups (oil pumps located within the same oil field). Ideally, there will be a customizable dashboard that shows crucial information at a glance. Fabrikam wants to know if there are out-of-the-box solutions for creating these visualizations and dashboards without involving developers and other IT staff.

Fabrikam has collected and compiled thorough maintenance and operational data of rod pump components, creating separate data sets for pumps operating under normal conditions, during gradual mechanical failure, and during periods of immediate failure. Each of the elements of the rod pump's mechanism generates a consistent pattern in their telemetry when operating under normal conditions. If one of these components starts to degrade or suffers an operational failure, the signal reflects this change in status. Fabrikam would like to use this historical data to train a Machine Learning (ML) model to predict when a pump needs to be maintained. They want to use this trained model to make predictions in real time, based on telemetry from their pumps' sensors. If the model predicts a pump needs to be maintained, they would like to automatically send an alert to engineers and field pump supervisors so they can potentially mitigate the issue and prevent damage to the failing and related components. In many cases, the fuel rod's onboard controller can modify the operating parameters of the pump to avoid or mitigate the impact of unexpected changes. Alternatively, if necessary, it can shut down the pump before any damage occurs and notify the company that repairs are necessary, protecting the machinery, and preventing potential environmental damage. Fabrikam would like to have a mechanism within their solution to send commands to rod pump controllers to modify these operating parameters remotely.

Their goal in the use of such predictive models is to increase operator efficiency and safety. Addressing a typical maintenance issue takes several people and at least three days of system downtime at a cost of up to \$20,000 USD a day, not including parts and labor. "By proactively identifying pump problems through predictive analytics, companies reduce unplanned downtime, which decreases costs, increases production, and increases the agility of maintenance services." says Fabrikam's Chief Engineer, Peter Guerin. He adds that the majority of industry accidents don’t happen at the well site, they happen when personnel are driving between sites. By eliminating the need for many site visits, they can reduce those accidents.

They would like to understand their options for expediting the implementation of the PoC. Specifically, they are looking to learn what offerings Azure provides that could enable a quick end-to-end start on the infrastructure for monitoring and managing devices and the system metadata. On top of this, they are curious about what other platform services Azure provides that they should consider in this scenario.

They would like to start by building a proof of concept that performs the predictive analytics in the cloud. While their machine learning will initially happen in the cloud, they would like to design their solution with an eye towards the future so it could be enhanced to run the models at the edge.

#### Telemetry data

Fabrikam identified 33 rod pump components whose telemetry they want to capture and monitor. Of these, they want to automatically monitor five that can be used to predict potential mechanical failure or detect an active failure.

| Field          | Type    | Description                                                                                                                                                                                                                                                  |
| -------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MotorPowerkW   | Numeric | Measured in Kilowatts (kW); The power output of the motor should be steady, but will drop if there is a problem                                                                                                                                              |
| MotorSpeed     | Numeric | Measured in RPM (including slip); Can change based on density of oil. Lower density causes this to go up (like if you have pockets of gas and it jumps up). If there's a failure it will go down below the normal operating average.                         |
| CasingFriction | Numeric | Measured in PSI (psi); The pressure will drop if a fissure is developing in the casing, indicating a failure.                                                                                                                                                |
| PumpRate       | Numeric | Speed calculated over the time duration between the last two times the crank arm has passed the proximity sensor measured in Strokes Per Minute (SPM) - minimum 0.0, maximum 100.0. A significant slowdown could be an indicator of failure within the pump. |
| TimePumpOn     | Numeric | Number of minutes the pump has been on. This should be a steady sawtooth pattern with a regular cadence of the pump cycling power. A consistently shorter than average cadence can indicate problems with the pump.                                          |

Normal signal readings from these five sensors appear in the chart below, with 10,000 intervals. The frequency of the output is condensed to fit:

![The five components' telemetry shown in their normal operating state.](media/normal-telemetry.png 'Normal telemetry')

The next chart shows the telemetry for these five components during a gradual failure. In many cases, there is time to react and prevent total failure through remote commands to the pump controller:

![The five components' telemetry shown during gradual failure.](media/gradual-failure-telemetry.png 'Gradual failure')

This final chart shows the telemetry for these five components when there is an immediate failure:

![The five components' telemetry during immediate failure.](media/immediate-failure-telemetry.png 'Immediate failure')

### Customer needs

1. We are interested in comparing SaaS and PaaS-based offerings on Azure. Based on our needs, will a SaaS solution meet our needs for a rapid PoC?

2. Need web-based access to metadata management of the rod pump devices for simplified management by our users.

3. When we expand beyond the PoC, we need to be able to add devices in bulk for our customers.

4. We would like to have configurable standard dashboards for all users and personalized dashboards.

5. Need collection and export of real-time telemetry, at scale. There should be an intuitive interface for analyzing collected data as it arrives, or within timelines to include historical information.

6. Require strong device security with encryption at transit and at rest, as well as ample cloud-based security and user management.

7. We want to use historical pump data to train a Machine Learning (ML) model to predict in real time whether a pump should be maintained to prevent failure. We'd like to periodically re-train the model with new data.

8. We want to configure alerts when the ML model predicts failure so engineers can take action and send remote commands to pump controllers to prevent damage due to mechanical failure. Alert options should be flexible for choosing a destination and executing automated tasks.

### Customer objections

1. Is there an out of the box solution we can use to jump-start the creation of the solution?

2. We are worried about being constrained by a "black box" if we go with a SaaS solution. Do we have access to all of our collected telemetry we can use for external workloads?

### Infographic for common scenarios

Use the following diagram for inspiration in your design.

![The infographic shows common scenarios for a SaaS and PaaS-based IoT architecture.](media/infographic.png 'Infographic for common scenarios')

## Step 2: Design a proof of concept solution

**Outcome**

Design a solution and prepare to present the solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 60 minutes

**Business needs**

Directions: With all participants at your table, answer the following questions and list the answers on a flip chart:

1. Who should you present this solution to? Who is your target customer audience? Who are the decision makers?

2. What customer business needs do you need to address with your solution?

**Design**

Directions: With all participants at your table, respond to the following questions on a flip chart:

_High-level architecture_

1. Without getting into the details (the following sections will address the particular details), diagram your initial vision for using a SaaS-based IoT solution on Azure with device management, custom dashboards, user management, real-time telemetry capture, analysis, and export. If you can, include the underlying architecture of the SaaS solution by identifying its major components.

_IoT options in Azure_

1. What are the SaaS-based IoT options in Azure?

2. What are the PaaS-based IoT options in Azure?

3. Would you recommend SaaS or PaaS for this customer situation? What are the pros and cons of each?

_Device and metadata management_

1. How do you connect devices one at a time?

2. How do you connect multiple devices at scale? What options are there to secure device connections?

3. When Fabrikam is ready to mass manufacture devices, can they configure their devices to automatically connect to the cloud when turned on, or do they all have to be registered during installation?

4. What communication protocols are supported? What if they are using devices that do not support those protocols?

5. Is there a way to define common metadata for devices, such as location and serial number? How is this metadata applied to devices, and how can developers set this metadata programmatically?

6. How can control messages be sent to rod pump controllers from the cloud to perform tasks like turn off the pump engine or change settings?

_Dashboards and telemetry analysis_

1. How would you propose Fabrikam create visualizations for each rod pump? What options are available to view and filter the device telemetry?

2. How can they create shared dashboards, and can users create their own personalized dashboards?

3. Can telemetry be automatically exported to external storage for offline batch processing? What other options are available to gain access to telemetry outside of the core IoT solution?

_Security_

1. Is device data encrypted both in transit and at rest?

2. Can Fabrikam use standard certificates for device authentication? How do Fabrikam's administrators approve new devices that attempt to connect to the cloud?

3. What user management options are available for the dashboards? What roles are defined?

_Alerts and integrations_

1. Fabrikam has historical telemetry data from pumps that operate under normal, gradually failing, and immediately failing conditions. They want to train a Machine Learning (ML) model with this data and use it for real-time anomaly detection. Which platform would you recommend for training and deploying the model?

2. How can Fabrikam make real-time predictions with the trained model and send alerts if needed? They are interested in available integrations that may work with services they already use, like Office 365 or Dynamics CRM.

**Prepare**

Directions: With all participants at your table:

1. Identify any customer needs that are not addressed with the proposed solution.

2. Identify the benefits of your solution.

3. Determine how you will respond to the customer's objections.

Prepare a 15-minute chalk-talk style presentation to the customer.

## Step 3: Present the solution

**Outcome**

Present a solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 30 minutes

**Presentation**

Directions:

1. Pair with another table.

2. One table is the Microsoft team and the other table is the customer.

3. The Microsoft team presents their proposed solution to the customer.

4. The customer makes one of the objections from the list of objections.

5. The Microsoft team responds to the objection.

6. The customer team gives feedback to the Microsoft team.

7. Tables switch roles and repeat Steps 2-6.

## Wrap-up

Timeframe: 15 minutes

Directions: Tables reconvene with the larger group to hear the facilitator/SME share the preferred solution for the case study.

## Additional references

| Description                                                           | Links                                                                                                |
| --------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| About IoT Central                                                     | <https://docs.microsoft.com/azure/iot-central/overview-iot-central>                                  |
| About IoT Hub                                                         | <https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub>                                   |
| What are IoT solution accelerators?                                   | <https://docs.microsoft.com/azure/iot-accelerators/iot-accelerators-what-are-solution-accelerators>  |
| Azure IoT Hub Device Provisioning Service (DPS)                       | <https://docs.microsoft.com/azure/iot-dps/about-iot-dps>                                             |
| Conceptual understanding of X.509 CA certificates in the IoT industry | <https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-concept>                                    |
| Creating a certificate chain when signing devices                     | <https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md> |
| IoT Central continuous data export to Event Hubs and Service Bus      | <https://docs.microsoft.com/azure/iot-central/howto-export-data-event-hubs-service-bus>              |
| IoT Central continuous data export to Blob Storage                    | <https://docs.microsoft.com/azure/iot-central/howto-export-data-blob-storage>                        |
| About Azure Blob storage                                              | <https://docs.microsoft.com/azure/storage/blobs/storage-blobs-overview>                              |
| About Azure Event Hubs                                                | <https://docs.microsoft.com/azure/event-hubs/event-hubs-about>                                       |
| What is Azure Databricks?                                             | <https://docs.microsoft.com/azure/azure-databricks/what-is-azure-databricks>                         |
| What is Azure Machine Learning service?                               | <https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml>                |
| Azure Kubernetes Service (AKS)                                        | <https://docs.microsoft.com/azure/aks/>                                                              |
| Azure functions                                                       | <https://docs.microsoft.com/azure/azure-functions/functions-overview>                                |
| Microsoft Power Automate                                                       | <https://flow.microsoft.com/>                                                                        |
| What is Azure Logic Apps?                                             | <https://docs.microsoft.com/azure/logic-apps/logic-apps-overview>                                    |
