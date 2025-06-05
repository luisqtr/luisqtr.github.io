---
layout: post
title: Excite-O-Meter
author: quintero
date: 2021-10-10 10:00:00 +0100
categories: [research, projects]
tags: [XR, ML, physio, unity, python]
published: true
comments: false
---

<!-- <img src="{{site.url}}/assets/img/portfolio/EoM.png" width="10%"> -->

A Software Framework to Integrate Physiological Data in Extended Reality Applications.

📃**Paper:** [Excite-O-Meter: Software Framework to Integrate Heart Activity in Virtual Reality, *ISMAR21*.](https://doi.org/10.1109/ISMAR52148.2021.00052)

⌨**Repository/Documentation:** <https://github.com/luisqtr/exciteometer>

📱**Windows 10/11 App:** <https://www.microsoft.com/store/apps/9PFMNFQJB99Q>

🖥**Project Website:** <http://exciteometer.eu/>

<!-- <img src="{{site.url}}/assets/img/portfolio/EoM/architecture.jpg" width="80%"> -->

![teaser]({{site.url}}/assets/img/portfolio/EoM/eom_teaser_github_banner.jpg){:width="80%"}

## Description

The `Excite-O-Meter` (`EoM`) is a package that extends a standalone Unity project with functionalities to easily record users' data in experimental sessions. It captures heart and motion activity, automatically extracts relevant data features, and visualizes the collected data directly in your compiled desktop application. Suitable for Unity developers wanting to analyze body responses from users or researchers conducting empirical studies in interactive applications with Unity.

The `EoM` enables the integation of heart activity and movement analysis in any standalone application created with Unity, intended for **Extended Reality (XR)**. This plugin contains all the logic to record data from external wearable sensors, log into persistent files, and visualize the captured data without leaving the Unity Editor. 

The tool is simple to use and doesn't require coding. The `EoM` is particularly suitable in two **use cases**: 1) for hobbyists or *Unity developers* wanting to measure the body responses that your application induces on your users. 2) for *researcher* running scientific experiments (e.g., psychology or behavioral research) in XR and wanting to easily collect data using a Unity environment that you created or found online.

The `EoM` may be used without external wearable sensors. However, the tool's main advantage is the easy integration with body sensors compatible with [LSL](https://github.com/sccn/labstreaminglayer). Currently, it is compatible with the chest strap sensor [Polar H10](https://www.polar.com/us-en/products/accessories/h10_heart_rate_sensor) to capture **heart rate (HR)** and heart rate variability data (HRV), *(see top-right image)*. It also records **movement** from any object in the scene, useful to record head movement from **Virtual Reality (VR)** headsets record headsets. Additionally, screenshots and manual string markers can be added to label specific events occurring while users interact with your XR environment. Finally, it includes a data visualizer to review the session of the user offline *(see bottom-right image)*, showing in synchrony all the time-series data, screenshots, and markers. Everything works in the Unity Editor and in the final **compiled** application.

