

# Guide to Using dSPACE ControlDesk and MicroNova EXAM for Automotive Test Automation

This guide is tailored for an experienced automotive test automation engineer with 15 years of experience using ETAS tools (e.g., INCA) and ECU-TEST. It provides practical steps to set up and use **dSPACE ControlDesk** and **MicroNova EXAM** for ECU testing, focusing on hardware-in-the-loop (HIL) simulation and test automation. The guide assumes familiarity with ECU testing concepts and draws parallels with ECU-TEST workflows.

## 1. Overview

### dSPACE ControlDesk
- **Purpose**: Experiment and instrumentation software for ECU development, used for rapid control prototyping (RCP), HIL simulation, measurement, calibration, and diagnostics.
- **Key Features**:
  - Unified interface for managing experiments, visualizing data, and interacting with dSPACE platforms (e.g., SCALEXIO).
  - Supports ASAM standards (e.g., CCP, XCP, ASAM MDF).
  - Automation via Python/C# scripts.
  - Photorealistic layouts for data visualization.
- **Comparison to ETAS INCA**: Like INCA, ControlDesk handles measurement and calibration, but it’s tightly integrated with dSPACE hardware and supports broader experiment management, including RCP and HIL.

### MicroNova EXAM
- **Purpose**: Test automation software for graphical test case development, widely used in automotive HIL testing (e.g., Volkswagen Group).
- **Key Features**:
  - Graphical test case design using UML (sequence/activity diagrams).
  - Platform-independent, reusable test cases.
  - Supports interfaces like dSPACE ControlDesk, Vector CANoe, and ETAS INCA.
  - Free core system with open-source libraries.
- **Comparison to ECU-TEST**: EXAM’s graphical test case development is similar to ECU-TEST’s test case editor, but EXAM emphasizes UML-based modeling and platform independence, while ECU-TEST is more tightly coupled with ETAS tools.

## 2. Prerequisites

- **Hardware**:
  - dSPACE HIL system (e.g., SCALEXIO) for ControlDesk.
  - ECU under test (real or virtual).
  - PC with sufficient specs (Windows 10/11, 16GB RAM recommended).
- **Software**:
  - **ControlDesk**: Install the Main Version (full functionality) from dSPACE’s website or Support Central. Ensure compatibility with your dSPACE platform (e.g., Release 2023-B).
  - **EXAM**: Download the free core system from MicroNova’s website (requires registration). Install core libraries and any required plugins (e.g., dSPACE interface).
  - **MATLAB/Simulink**: For model-based development (similar to your ETAS workflow).
  - **Python**: For automation scripts in ControlDesk (optional).
- **Access**:
  - dSPACE Support Central (documentation, tutorials).
  - MicroNova EXAM user area (webinars, downloads; requires login).
- **Knowledge**: Familiarity with CAN bus, XCP/CCP protocols, and HIL testing (assumed from your experience).

## 3. Setting Up ControlDesk

### Installation
1. **Download and Install**:
   - Access dSPACE’s Support Central or contact your dSPACE representative for the ControlDesk installer.
   - Install the Main Version (not Operator Version) for full functionality.
   - Verify compatibility with your dSPACE platform (e.g., SCALEXIO, VEOS).
2. **Configure Hardware**:
   - Connect your dSPACE HIL system (e.g., SCALEXIO) to the PC.
   - Use dSPACE ConfigurationDesk to set up the HIL platform (e.g., load Simulink models, configure I/O).
3. **Initial Setup**:
   - Launch ControlDesk.
   - Create a new project: `File > New > Project`.
   - Link to your dSPACE platform via the Platform/Device Manager.
   - Import a Simulink model (e.g., a control model for an ECU) or use a template (e.g., ADCtemplate.mdl).

### Basic Usage
1. **Create an Experiment**:
   - Go to `File > New > Experiment`.
   - Select your platform and model.
   - Configure variables to measure (e.g., ECU signals like engine speed).
2. **Build a Layout**:
   - Use the Instrumentation tab to create a virtual instrument panel.
   - Drag and drop widgets (e.g., plots, gauges) to visualize signals.
   - Example: Add a plot to monitor a CAN signal (e.g., vehicle speed).
3. **Measurement and Calibration**:
   - Use the Variable Explorer to select ECU variables (via XCP/CCP, similar to INCA).
   - Start a measurement: `Measurement > Start`.
   - Adjust parameters in real-time (e.g., throttle position) using sliders or numeric inputs.
4. **Automation**:
   - Write Python scripts to automate tasks (e.g., start/stop measurements).
   - Example script to start a measurement:
     ```python
     import dspace.controlDesk
     experiment = dspace.controlDesk.getActiveExperiment()
     experiment.startMeasurement()
     ```
   - Save scripts in the Automation tab for reuse.

### Tips for ECU-TEST Users
- **Similarities**: ControlDesk’s Variable Explorer is akin to ECU-TEST’s variable management. Layouts are similar to ECU-TEST’s visualization panels.
- **Differences**: ControlDesk is more hardware-centric (tied to dSPACE platforms) and supports broader experiment management (e.g., RCP).
- **Learning Curve**: Focus on the Platform/Device Manager and Instrumentation tab, as these differ from ETAS’s workflow.

## 4. Setting Up EXAM

### Installation
1. **Download and Install**:
   - Register at MicroNova’s website (www.micronova.de) to access the EXAM user area.
   - Download the free core system and core libraries.
   - Install plugins for dSPACE ControlDesk integration.
2. **Configure Interfaces**:
   - In EXAM, go to `Settings > Interfaces`.
   - Add the dSPACE ControlDesk interface (requires ControlDesk to be installed).
   - Configure other interfaces as needed (e.g., CANoe, INCA for cross-tool compatibility).
3. **Project Setup**:
   - Create a new test project: `File > New Project`.
   - Define the test environment (e.g., link to SCALEXIO via ControlDesk).

### Basic Usage
1. **Create a Test Case**:
   - Open the Test Case Editor.
   - Use UML sequence or activity diagrams to model a test case (drag-and-drop interface, similar to ECU-TEST’s graphical editor).
   - Example: Create a sequence to send a CAN signal (e.g., throttle = 50%) and check the ECU’s response (e.g., engine RPM).
2. **Map Signals**:
   - Link test case variables to ECU signals via ControlDesk (using XCP/CCP).
   - Example: Map “throttle_input” to a CAN signal in ControlDesk’s Variable Explorer.
3. **Execute Tests**:
   - Run the test case: `Test > Run`.
   - EXAM communicates with ControlDesk to send signals and collect data.
   - Results are logged in ASAM MDF format (similar to ECU-TEST’s logging).
4. **Automation**:
   - Use EXAM’s Test Manager to automate test sequences across multiple ECUs or variants.
   - Reuse test cases across projects (EXAM’s platform independence is a key advantage over ECU-TEST).

### Tips for ECU-TEST Users
- **Similarities**: EXAM’s graphical test case editor is very similar to ECU-TEST’s, and both support ASAM standards and HIL testing.
- **Differences**: EXAM’s UML-based approach is more standardized and platform-agnostic, while ECU-TEST is optimized for ETAS ecosystems.
- **Learning Curve**: Focus on EXAM’s interface configuration and UML editor. Leverage your ECU-TEST experience for test case design.

## 5. Integrating EXAM with ControlDesk

1. **Setup**:
   - Ensure ControlDesk is running and connected to the dSPACE platform.
   - In EXAM, configure the dSPACE interface to point to ControlDesk’s API.
2. **Workflow**:
   - Design test cases in EXAM (e.g., send a CAN signal and verify ECU output).
   - Use ControlDesk to execute the test on the HIL system and visualize results.
   - Example: EXAM sends a throttle signal via ControlDesk, which applies it to the ECU and plots the response (e.g., RPM).
3. **Automation**:
   - Create a test suite in EXAM to run multiple test cases.
   - Use ControlDesk’s Python API to automate data collection or layout updates during testing.

## 6. Example Workflow: Testing an ECU’s CAN Response

**Scenario**: Test an ECU’s response to a CAN throttle signal (50% throttle should yield 3000 RPM).

### Step 1: ControlDesk Setup
1. Open ControlDesk and create a new project.
2. Link to a SCALEXIO platform with a Simulink model of the ECU.
3. In the Variable Explorer, map:
   - Input: `throttle_input` (CAN signal).
   - Output: `engine_rpm` (ECU response).
4. Create a layout with:
   - A numeric input for `throttle_input`.
   - A plot for `engine_rpm`.
5. Test manually: Set `throttle_input = 50%` and verify `engine_rpm ≈ 3000`.

### Step 2: EXAM Test Case
1. Open EXAM and create a new test project.
2. In the Test Case Editor, create a sequence diagram:
   - Step 1: Set `throttle_input = 50%` via ControlDesk.
   - Step 2: Wait 1 second.
   - Step 3: Read `engine_rpm` via ControlDesk.
   - Step 4: Assert `engine_rpm` is within 2900–3100 RPM.
3. Map signals to ControlDesk variables (`throttle_input`, `engine_rpm`).
4. Run the test case. EXAM sends the signal via ControlDesk and logs results.

### Step 3: Automation
1. In EXAM, create a test suite with multiple throttle values (e.g., 25%, 50%, 75%).
2. In ControlDesk, write a Python script to log results to an MDF file:
   ```python
   import dspace.controlDesk
   experiment = dspace.controlDesk.getActiveExperiment()
   experiment.startRecording("test_results.mdf")
   ```
3. Execute the suite in EXAM, which triggers ControlDesk to run tests and save data.

## 7. Resources and Training

- **ControlDesk**:
  - **Training**: Enroll in dSPACE’s ControlDesk Basic (€850/$1200, 1-2 days) or Advanced (€850) courses. Upcoming sessions: September 9-10, 2025 (virtual), October 14, 2025 (Paderborn). Expect hands-on assessments.
  - **Resources**: dSPACE Support Central (FAQs, videos, documentation).
- **EXAM**:
  - **Training**: Contact MicroNova for “Automated Tests with EXAM” (check user area for schedules). Includes practical exercises.
  - **Resources**: MicroNova EXAM user area (webinars, downloads; requires login).
- **Self-Study**:
  - Practice with dSPACE templates (e.g., ADCtemplate.mdl).
  - Use EXAM’s free core system to experiment with test cases.
  - Compare workflows with ECU-TEST to accelerate learning.

## 8. Tips for Success
- **Leverage ETAS Experience**: Your ECU-TEST and INCA skills (e.g., signal mapping, test automation) directly apply to EXAM’s test case design and ControlDesk’s measurement workflows.
- **Start Small**: Begin with a single test case in EXAM and a simple layout in ControlDesk to understand the integration.
- **Automate Early**: Use EXAM’s Test Manager and ControlDesk’s Python API to streamline repetitive tasks, similar to ECU-TEST’s automation capabilities.
- **Community Support**: Engage with MicroNova’s EXAM user community (e.g., Volkswagen Group users) or dSPACE forums for best practices.

## 9. Next Steps
- **ControlDesk**: Experiment with layouts and automation scripts. Attend dSPACE’s Basic training for hands-on guidance.
- **EXAM**: Build a sample test case and test it on a dSPACE platform. Explore MicroNova’s webinars for advanced features.
- **Integration**: Practice linking EXAM test cases to ControlDesk for a real HIL setup.

For further assistance, contact:
- **dSPACE**: Support Central or training@dspace.de.
- **MicroNova**: EXAM user area or info@micronova.de.

Happy testing!

