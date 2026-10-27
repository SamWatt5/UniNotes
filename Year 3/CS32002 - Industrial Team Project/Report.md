# Introduction
This section should introduce the project. It should include an explanation of the problem and the objectives of the project. It is very important to give a clear description of what the project is actually intended to do, preferably in non-technical terms
## Explanation of Problem
Atms produce lots of different logs in various formats from various sources. software logs, operating system metrics, event streams, hardware health, cloud metrics. Task is to create a log aggregation and analysis platform. ingest data from the multiple sources, identify anomalies, present insights, clear interface. 
## Objectives of Project
industry-inspired prototype that aggregates and analyses heterogeneous logs while respecting strict data-security constraints.
### multi source log ingestion
Generate synthetic logs based on data dictionaries
Accept logs from multiple channels
### Analysis & Pattern Detection
Provide meaningful analysis such as detecting anomalies, correlating events across log types, and identifying indicators of problems. 
### Visualisation & Reporting
Provide dashboards and views for charts, timelines and summaries of key events. Highlight detected anomalies or risk conditions clearly.
### Intelligent Diagnostic Recommendation Engine
provide automated, intelligent recommendations for possible causes and suggested remediation steps. Provide a probable root cause, recommended next actions.
## Clear description of what project is intended to do
There are almost 50,000 ATMs in the UK[https://commonslibrary.parliament.uk/research-briefings/cbp-8570/], with the average UK adult withdrawing £1352 from these cash machines in 2025[https://www.link.co.uk/news/average-uk-adult-withdrew-1-352-from-atms-in-2025]. If any issue occurs on an ATM, there is immediate impact, with customers losing access to cash and creating a loss of trust in the service. To identify any such problems, ATMs produce data from various sources, such as software logs, operating system metrics, hardware health indicators and event streams. These logs are used to provide meaningful insights for ATM managers to understand any issues that arise in their ATM network. The aim of this project was to create a system that aggregates these logs, provides meaningful analysis on the data, then presents the information clearly. There were four main requirements to this project:
1. Multi-Source Log Ingestion
	The system must be able to accept logs from multiple sources. Due to the protected nature of real NCR Atleos data, it cannot be used, and instead, synthetic log data must be generated from provided data dictionaries.
2. Analysis & Pattern Detection
	From the ingested logs, analysis must be performed. This may include detecting anomalies, correlating events across sources, and identifying indicators of problems.
3. Visualisation and Reporting
	The system must display dashboards and views. These could include charts, timelines and summaries of key events. The system must also clearly highlight detected anomalies.
4. Intelligent Diagnostic Recommendations
	The system should also be able to provide automated recommendations for possible root causes of anomalies, and suggested actions.
Beyond these four core requirements, the technology choices the project team could use were open, and third-party libraries were allowed, as long as they were free for commercial use.
The project team was given 3 weeks to develop this system, including design, development, testing and evaluation.
The goal of this report is to document the project team's development process for this system, including design decisions, implementation strategies, testing and evaluation, and finally a conclusion.
# Summary & Conclusion
Summarise the main points of what you have achieved in your project and the main conclusion(s) that can be drawn. This should include a critical appraisal of the project where you reflect on any lessons learnt during the course of the project with the benefit of hindsight, e.g. would you do anything differently if you could do the entire project again? Did all of your decisions work out? Did your project go according to plan? What would you recommend to others? Please also consider what the main learning outcomes have been for you from the project. Finally, you should also make recommendations for future work.
## Main points of what we achieved
We designed a log aggregation, analysis and diagnostics platform. It ingests logs from across multiple channels, and identifies anomalies in the data. these anomalies are analysed, finding a root cause, as well as recommended next steps. These anomalies and the relevant analysis is displayed on  a clear frontend.
## Critical appraisal
### Reflect on lessons learns
#### would we do anything differently?
Spend less time on requirements, and get developing faster
#### Did all of our decisions work out?
We initially decided to use a kanban board to write tasks, but after a week of the project, we realised we hadnt been using it.

#### Did our project go according to plan?
yes, our project went according to plan, we implemented everything we wanted to, and didnt 
#### What would I recommend to others?
would recommend t
### Main learning outcomes from the project
## Recommendations for future work
Looking forward with this system, the project team would implement predictive detection, using a lightweight ML model, predicting when anomaly might occur before it does. Another feature the project team would implement, if they had more development time, would be to allow real time log ingestion, detecting anomalies as they occur. One more feature the team would implement would be to make the system less ATM-specific, allowing any logging to be processed by the system automatically.
## Actual
The project team successfully built a working log aggregation, analysis and diagnostics platform within three weeks, meeting all four core requirements. The system which the team created ingests synthetic logs from multiple sources, detects the seven defined anomaly types, ranks them by criticality, using a weighted scoring system, and finally presents these anomalies, along with recommended actions, through a clear user interface. 
The team felt that throughout the project, their communication was failing them, and if the team were to do the project again they would utilise agile techniques to improve their understanding of each other's roles in the system, as well as having a clearer, stricter allocation of tasks. One solution that could be used to improve team communication would be to use a Kanban board to keep track of tasks. This would help by providing a visual overview of what needs to be done during each sprint of development, as well as what has been achieved by the team so far. The team would also plan their sprints more, understanding exactly what needs to be done at the beginning of each week. This would help as the team felt that sprints two and three blended into one. This caused problems because without any clear focus, it was difficult to understand what features needed to be implemented and prioritised.
One of the aspects of this project that the team was most proud of was the depth of the system testing, with 48 passing tests across the system, finding real issues that could be solved quickly, without creating technical debt. The project team is also proud of the security of the system, using JWT authentication, and implementing role-based access to allow system admins to have extra control over the system functionality. Another aspect of the development process that the team is proud of is the effectiveness in response to client and user feedback, implementing real changes when a feature wasn't understood or used correctly.
Beyond what was achieved, the project team had some ideas for what they could implement in the system, given more time. Firstly, the team would implement predictive detection, using a lightweight ML model, predicting when an anomaly might occur before it does. Another feature the project team would implement would be to allow real time log ingestion, detecting anomalies as they occur. One more feature the team would implement would be to make the system less ATM-specific, allowing any logging to be processed by the system automatically.
Overall, the project gave the team valuable experience working in an industrial-style agile team, responding to real client requirements under time pressure, which are skills that are crucial for professional software development.


# Meeting Minutes
## Week 1 Management - 18/3/25 15:00-15:15
### Attendance
Sam Watts, Emmanuel Dairo, Sarah Kelly, Addie Tweed, Martin Kelly, Ahmed Ikram, David Hyacinth-Ngwu
### Discussion
The team provided an update on progress during the first week. The team mentioned they were working on system design. The manager noted that they were progressing too slow, and should start writing code before the week's end.
### Feedback
The manager advised the team to accelerate progress and begin development before the end of the week.
## Week 2 Client - 23/3/25 10:30-10:50
### Attendance
Sam Watts, Emmanuel Dairo, Sarah Kelly, Addie Tweed, Martin Kelly, Ahmed Ikram
### Discussion
The team presented the system requirements to the client, who were satisfied. The initial wireframes for the dashboard and data analysis page were shown. The client responded positively to the design, noting the clarity and lack of clutter.
### Feedback
The client advised that the system should not be too ATM-specific, and that anomalies should extend to other systems such as servers and operating systems.
## Week 2 Management - 23/3/25 15:20-15:35
### Attendance
Sam Watts, Emmanuel Dairo, Sarah Kelly, Addie Tweed, Martin Kelly, Ahmed Ikram
### Discussion
The team provided an update on development progress during week 2
### Feedback
The manager reminded the team to begin working on the project report. The manager also made sure that the team were to complete a user evaluation of the system.
## Week 3 Client - 30/3/25 13:00-13:20
### Attendance
Emmanuel Dairo, Sarah Kelly, Addie Tweed, Martin Kelly, Ahmed Ikram
### Discussion
The project team showed the client the completed system, walking through each component in detail. The client asked if the team could implement AI pattern detection before the presentation. The team responded saying they would consider it if they had finished the whole system before Wednesday. The client was satisfied with the demonstration and sought clarification on some aspects of the system, which the team addressed.
## Week 3 Management - 30/3/25 15:35-15:50
### Attendance
Emmanuel Dairo, Sarah Kelly, Addie Tweed, Martin Kelly, Ahmed Ikram
### Discussion
The team discussed with the manager how they felt the meeting with the client had gone. They reported feeling it went well. The manager also said he thought it went well and he liked the way the team handled the client request to implement the AI pattern detection professionally. The team asked about whether the user evaluation should be recorded, and the manager responded saying that the evaluation should not, and participant responses must be kept fully anonymous.
### Feedback
The manager advised the team to focus on completing the report and preparing for the presentation.