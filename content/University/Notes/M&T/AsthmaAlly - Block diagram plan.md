---
tags:
  - y2s3-MnT
status: Ongoing
cssclasses:
  - wide-page
---
# Hello!
Read on to explore the block diagram that maps out our project pathways!
[[AsthmaAlly_block_diagram.excalidraw|excalidraw link]]
## The Block Diagram
![[AsthmaAlly_block_diagram.excalidraw.png]]

## The Gantt Diagram
```mermaid
---
config:
  theme: forest
---
gantt
  title AsthmaAlly Gantt Chart
  dateFormat  YYYY-MM-DD
  axisFormat  %b %d, %Y
  section Amar
  Define UI & App Requirements                   :2025-05-05, 2025-05-12
  Design App Wireframes & User Flow              :2025-05-12, 2025-05-19
  Develop App Frontend Prototype                 :2025-05-19, 2025-06-02
  Develop Back-end Data Interface                :2025-05-26, 2025-06-09
  Integrate App With Embedded System             :2025-06-09, 2025-06-19
  Implement User/Caretaker Alert System          :2025-06-19, 2025-07-03
  Final App Testing & Polishing                  :2025-07-03, 2025-07-17
  Prepare App for Release                        :2025-07-17, 2025-08-01

  section Vanessa
  Research Ergonomic Wearable Concepts           :2025-05-05, 2025-05-12
  Chest Sensor - ID & Prototyping                :2025-05-12, 2025-05-26
  Wrist Sensor - ID & Prototyping                :2025-05-26, 2025-06-09
  User Testing & Design Refinement               :2025-06-09, 2025-06-19
  Finalize Mechanical Design (Chest/Wrist)       :2025-06-19, 2025-07-03
  Support Integration With Electronics           :2025-07-03, 2025-07-17

  section Dakshita
  Define Data Requirements & Model Use Cases     :2025-05-05, 2025-05-12
  Gather & Process Hospital Training Data        :2025-05-12, 2025-05-26
  Feature Selection (Data from Devices)          :2025-05-26, 2025-06-02
  Initial Model Development                      :2025-06-02, 2025-06-16
  Train Model & Validate                        :2025-06-16, 2025-07-03
  Integrate ML Model With Application            :2025-07-03, 2025-07-17
  Full System Testing & Final Model Tuning       :2025-07-17, 2025-08-01

  section Dylan
  Investigate sensor technologies                :2025-05-05, 2025-05-12
  Create circuit diagram                         :2025-05-12, 2025-05-15
  Collate bill of material                       :2025-05-15, 2025-05-21
  Assemble breadboard circuit                    :2025-05-21, 2025-05-26
  Write and test embedded system code            :2025-05-26, 2025-06-12
  Evaluate points of improvement                 :2025-06-12, 2025-06-15
  Collate bill of material V2                    :2025-06-15, 2025-06-19
  Refine embedded system code                    :2025-06-19, 2025-07-03
  Embed circuitry into design                    :2025-07-03, 2025-07-10
  Implement UART to application                  :2025-07-10, 2025-07-17
  Troubleshooting and tuning                     :2025-07-17, 2025-08-15
```