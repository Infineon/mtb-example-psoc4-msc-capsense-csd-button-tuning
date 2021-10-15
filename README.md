# PSoC&trade; 4: MSC CAPSENSE&trade; CSD button tuning

This code example demonstrates how to use the CAPSENSE&trade; middleware to detect a finger touch on a self-capacitance-based Button widget in PSoC&trade; 4 devices with Multi sense converter (MSC).

In addition, this Readme also explains how to manually tune the self-capacitance-based button for optimum performance w.r.t parameters such as reliability, power consumption, response time and linearity using the CSD-RM sensing technique and CAPSENSE&trade; tuner GUI. Here,  CSD (CAPSENSE&trade; Sigma Delta) represents the self-capacitance sensing technique and RM represents the ratiometric method.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-msc-capsense-csd-button-tuning)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzEwNzgiLCJTcGVjIE51bWJlciI6IjAwMi0zMTA3OCIsIkRvYyBUaXRsZSI6IlBTb0MmdHJhZGU7IDQ6IE1TQyBDQVBTRU5TRSZ0cmFkZTsgQ1NEIGJ1dHRvbiB0dW5pbmciLCJyaWQiOiJibHBkIiwiRG9jIHZlcnNpb24iOiIyLjAuMCIsIkRvYyBMYW5ndWFnZSI6IkVuZ2xpc2giLCJEb2MgRGl2aXNpb24iOiJNQ0QiLCJEb2MgQlUiOiJJQ1ciLCJEb2MgRmFtaWx5IjoiUFNPQyJ9)


## Requirements

- [ModusToolbox&trade; software](https://www.cypress.com/products/modustoolbox-software-environment) v2.4 or later

   **Note:** This code example version requires ModusToolbox&trade; software version 2.4 or later, and is not backward compatible with v2.3 or older versions.

- Board support package (BSP) minimum required version: 2.0.0
- Programming language: C
- Associated parts: [PSoC&trade; 4100S Max](https://www.cypress.com/documentation/datasheets/psoc-4-psoc-4100s-max-datasheet-programmable-system-chip-psoc)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm® Embedded Compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm compiler v6.13 (`ARM`)
- IAR C/C++ compiler v8.42.2 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 4100S Max pioneer kit](https://www.cypress.com/documentation/development-kitsboards/psoc-4100s-max-pioneer-kit-cy8ckit-041s-max) (`CY8CKIT-041S-MAX`) - Default target

## Hardware setup

This example uses the board's default configuration. See the [Kit user guide](https://www.cypress.com/file/520036/download) to ensure that the board is configured correctly to VDDA at 5V (J10 should be at position 1 and 2). If you are using the code example at a VDDA voltage other than 5 V, ensure to set up the device power voltages correctly for the proper operation of the device power domains.  See [Steps to setup the VDDA supply voltage in Device configurator](#steps-to-setup-the-vdda-supply-voltage-in-device-configurator) for more details.

## Software setup

This example requires no additional software or tools.

## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade; software</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox Application**). This launches the [Project Creator](https://www.cypress.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.cypress.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can use the Library manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.cypress.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/ide_{version}/docs/mt_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; software provides the Project Creator as both a GUI tool and a command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

This tool has the following arguments:

Argument | Description | Required/optional
-----------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`target-dir`   | Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional
<br>

The following example will clone the "[PSoC&trade; 4: MSC CAPSENSE&trade; CSD button tuning](https://github.com/Infineon/mtb-example-psoc4-msc-capsense-csd-button-tuning)" application with the desired name "MSC CSD button tuning" configured for the *CY8CKIT-041S-MAX* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CKIT-041S-MAX --app-id mtb-example-psoc4-msc-capsense-csd-button-tuning --user-app-name MSCCSDButtonTuning --target-dir "C:/mtb_projects"
   ```

**Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For more details, see the "Project creator tools" section of the [ModusToolbox&trade; software user guide](https://www.cypress.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.cypress.com/ModusToolboxProjectCreator) tool:**

   1. Launch Project Creator from the Windows start menu or from *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/project-creator.exe*.
   2. In the initial **Choose Board Support Package** screen, select the BSP and click **Next**.
   3. In the **Select Application** screen, select the specific IDE from the **Target IDE** drop-down menu.
   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application, and import the libraries using the `make getlibs` command.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.cypress.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

The project already has the necessary settings by default, so you can go to [Operation](#operation) to test the example. If you want to understand the tuning process and follow the stages for this kit or your own board, go to [Tuning procedure](#tuning-procedure) and then test it using [Operation](#operation).

## Operation

1. Connect the board to your PC using the provided micro USB cable through the KitProg3 USB connector on J8 as follows:

   **Figure 1. Connecting the CY8CKIT-041S-MAX to a computer**

   <img src="images/kit_connection.jpg" alt="Figure 1"/>

2. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE for ModusToolbox&trade;</b></summary>

      1. Select the application Project in the Project Explorer.

      2. In the **Quick panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
      </details>

   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. You can specify a target and toolchain manually:
      ```
      make program TARGET=<BSP> TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TARGET=CY8CKIT-041S-MAX TOOLCHAIN=GCC_ARM
      ```
   </details>

3. After programming, the application starts automatically.

4. To test the application, place your finger over the CAPSENSE&trade; button and notice that the user LED turns ON when touched and turns OFF when the finger is lifted.

5. You can also monitor the CAPSENSE&trade; data using the CAPSENSE&trade; tuner application as follows:

    **Monitor data using CAPSENSE&trade; tuner**

    1. Open CAPSENSE&trade; tuner from the tools section in the IDE Quick panel. 
    
        You can also run the CAPSENSE&trade; tuner application standalone from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-tuner*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/COMPONENT_CUSTOM_DESIGN_MODUS/TARGET_\<BSP-NAME>* folder. 

	     See the [ModusToolbox&trade; user guide](https://www.cypress.com/ModusToolboxUserGuide) (locally available at *ModusToolbox install directory}/docs_{version}/mtb_user_guide.pdf*)for options to open the CAPSENSE&reg; tuner application using the CLI.

    2. Ensure the kit is in CMSIS-DAP bulk mode (KitProg3 Status LED is ON and not blinking). See [Firmware-loader](https://github.com/Infineon/Firmware-loader) to learn on how to update the firmware and switch modes in KitProg3.
  
    3. In the tuner application, click on the **Tuner communication setup** icon or select **Tools** > **Tuner communication setup**. In the window that appears, select the I2C checkbox under KitProg3 and configure as follows:

       - **I2C address:** 8
       - **Sub-address:** 2 bytes
       - **Speed (kHz):** 400

        These are the same values set in the EZI2C resource.

        **Figure 2. Tuner communication setup parameters**

        <img src="images/tuner-comm-setup.png" alt="Figure 2"/>

    4. Click **Connect** or select **Communication** > **Connect** to establish a connection.

        **Figure 3.Establish connection**

        <img src="images/tuner-connect.png" alt="Figure 3" width="400" />

    5. Click **Start** or select **Communication** > **Start** to start data streaming from the device.

         **Figure 4. Start tuner communication**

         <img src="images/tuner-start.png" alt="Figure 4" width="400" />

         The *Widget/Sensor parameters* tab gets updated with the parameters configured in the *CAPSENSE&trade; configurator* window. The tuner displays the data from the sensor in the **Widget view** and **Graph view** tabs.

    6.  Set the **Read mode** to Synchronized mode. Navigate to the  **Widget view** tab, you can see the **Button0** widget highlighted in blue color when you touch it.

         **Figure 5. Widget view of the CAPSENSE&trade; tuner**

         <img src="images/tuner-widget-view.png" alt="Figure 5"/>

    7. You can view the raw count, baseline, difference count and status for each sensor in the **Graph view** tab. For example, to view the sensor data for Button 0, select **Button0_Sns0** under **Button0**.

       **Figure 6. Graph view of the CAPSENSE&trade; tuner**

       <img src="images/tuner-graph-view-intro.png" alt="Figure 6"/>

    8. Observe the **Widget/Sensor parameters** section in the CAPSENSE&trade; tuner window as shown in **Figure 6**.
      
   9. Switch to the **SNR measurement** tab for measuring the SNR and verify that the SNR is above 5:1, select **Button1** and **Button1_Sns0** sensor, and then click **Acquire noise** as **Figure 7** shows.

      **Figure 7. CAPSENSE&trade; tuner - SNR measurement: acquire noise**

      <img src="images/tuner-acquire-noise.png" alt="Figure 7"/>

   10. Once the noise is acquired, place the metal finger at a position on the button and then click **Acquire signal**. Ensure that the metal finger remains on the button as long as the signal acquisition is in progress. Observe the SNR is above 5:1.

         The calculated SNR on this button is displayed, as **Figure 8** shows. Based on your end system design, test the signal with a finger that matches the size of your normal use case. Typically, finger size targets are ~8 to 9 mm. Consider testing with smaller sizes that should be rejected by the system to ensure that they do not reach the finger threshold.

         **Figure 8. CAPSENSE&trade; tuner - SNR measurement: acquire signal**

         <img src="images/tuner-acquire-signal.png" alt="Figure 8"/>

</details>

<br>

## Tuning procedure

<details><summary><b> Create custom BSP for your board </b></summary>

1. Create a custom BSP for your board having any device, by following the steps given in [KBA231373](https://community.cypress.com/t5/Knowledge-Base-Articles/ModusToolbox-2-2-and-later-Make-a-Custom-BSP-KBA231373/ta-p/251107).In this code example, it was created for the device "CY8C4149AZI-S598".

2. Open the *design.modus* file from *{Application root directory}/TARGET_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS* folder obtained in the previous step and enable CAPSENSE&trade; to get *design.cycapsense* file. CAPSENSE&trade; configuration can then be started from scratch as explained below.

</details>

The following steps explain the tuning procedure. 

**Note:** See the section "Selecting CAPSENSE&trade; hardware parameters" in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.cypress.com/AN85951) to learn about the considerations for selecting each parameter values.

**Figure 9. CSD button widget tuning flow**  

<img src="images/tuning-flowchart.png" alt="Figure 9" width="600" />

Do the following to tune the button widget:

<details> <summary><b>Stage 1: Set the initial hardware parameters</b> </summary>

1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.
2. Launch the Device configurator tool.

   You can launch the Device configurator in Eclipse IDE for ModusToolbox&trade; from the Tools section in the IDE Quick panel or in stand-alone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/device-configurator/device-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.modus* file of the respective application, which is present in the *{Application root directory}/COMPONENT_CUSTOM_DESIGN_MODUS/TARGET_\<BSP-NAME>* folder.

      **Note**: If you are using the custom BSP with the Empty PSoC&trade; 4 starter application, use *{Application root directory}/TARGET_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS* folder to open the *design.modus* file.

3. In the [CY8CKIT-041S MAX kit](https://www.cypress.com/documentation/development-kitsboards/psoc-4100s-max-pioneer-kit-cy8ckit-041s-max), the button pins are connected to both channel 0 and channel 1. Hence, make sure to enable channel 0 and channel 1 in the Device configurator as shown in **Figure 10**.

   **Figure 10. Enable MSC channels in device configurator**

   <img src="images/device-configurator.png" alt="Figure 10"/>

      Save the changes and close the window.

4. Launch the CAPSENSE&trade; configurator tool.
   
   You can launch the CAPSENSE&trade; configurator tool in Eclipse IDE for ModusToolbox&trade; from the 'CAPSENSE&trade;' peripheral setting in the device configurator or directly from the Tools section in the IDE Quick panel. You can also launch it in stand-alone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/COMPONENT_CUSTOM_DESIGN_MODUS/TARGET_\<BSP-NAME>* folder.

   **Note**: If you are using the custom BSP with the Empty PSoC&trade; 4 starter application, use *{Application root directory}/TARGET_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS* folder to open the *design.cycapsense* file.

   See the [ModusToolbox&trade; CAPSENSE&trade; configurator tool guide](https://www.cypress.com/ModusToolboxCapSenseConfig) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in ModusToolbox&trade;. 

5. In the **Basics** tab, note that two button widgets ‘Button0’ and 'Button1' is configured as a CSD RM (self-cap) and the CSD tuning mode is set as *Manual tuning*.

   **Figure 11. CAPSENSE&trade; configurator - basics tab**

   <img src="images/basic-csd-settings.png" alt="Figure 11"/>

6. Do the following in the General tab under the Advanced tab:

   - Set **Scan mode** as **INT driven**.

   - Set **Sensor connection method** as **CTRLMUX**. 

      **Note:** Use CTRLMUX if your schematic has all the sensors on ctrlmux pins. CTRLMUX mode allows the MSC block to control the GPIO pins and removes the need of AMUXBUS to transfer CAPSENSE&trade; signals between GPIO and the MSC block.

   - **Modulator clock divider** is set to **1** to obtain the maximum available modulator clock frequency as recommended in the [CAPSENSE&trade; design guide](https://www.cypress.com/AN85951). 

      **Note:** The modulator clock frequency can be set to 48,000 kHz only after changing the IMO clock frequency to 48 MHz, since the modulator clock is derived from the IMO clock. Do the following:

      1. Under the **System** tab in the **Device configurator** tool, select **System clocks** > **Input** > **IMO**. 

      2. Select **48** from the **Frequency(MHz)** drop-down list.

   - **Number of init sub-conversions** is set based on the hint shown when you hover over the edit box. Retain default value (will be set in **Stage 3**) 

   - Check the Enable self-test library selection. This is required for sensor capacitance measurement using BIST.
   
   - Retain the default settings for all filters. You can enable the filters later depending on the signal-to-noise ratio (SNR) requirements in **Stage 4**.
      
      Filters are used to reduce the peak-to-peak noise. Using filters will result in higher scan time.

   **Figure 12. CAPSENSE&trade; configurator - General settings**

   <img src="images/advanced-general-settings.png" alt="Figure 12"/>

   **Note:** Each Tab has a button **Restore Defaults** to restore the parameters of that Tab to their default values.

7. Go to the **CSD settings** tab and make the following changes:

   - Set **Inactive sensor connection** as **Ground**.

   - Select **Enable CDAC auto-calibration** and **Enable compensation CDAC**. 

      This helps in achieving the required CDAC calibration levels (85% of maximum count) for all sensors in the widget while maintaining the same sensitivity across the sensor elements.

   **Figure 13. CAPSENSE&trade; configurator - Advanced CSD settings**

   <img src="images/advanced-csd-settings.png" alt="Figure 13"/>

8. Go to the **Widget details** tab. Select **Button0** and **Button1** from the left pane, and then set the following:

   - **Sense clock divider:** Retain default value (will be set in **Stage 3**)

   - **Clock source:** **Direct**

      **Note:** Spread spectrum clock (SSC) or PRS clock can be used as a clock source to deal with EMI/EMC issues.


   - **Number of sub-conversions: 60**

     60 is a good starting point to ensure a fast scan time and sufficient signal. This value will be adjusted as required in **Stage 4**.

   - Select **Enable CDAC dither** 

   - **Finger Threshold:** 20

   - **Noise Threshold:** 10

   - **Negative Noise Threshold:** 10 

   - **Hysteresis:** 5

     These values reduces the influence of baseline on the sensor signal, which helps to get the true difference-count. Retain the default values for all other threshold parameters; these parameters are set in **Stage 5**.

   **Figure 14. CAPSENSE&trade; configurator - Widget details tab under the Advanced tab**  
      
   <img src="images/advanced-widget-settings.png" alt="Figure 14" />

9. Go to the **Scan configuration** tab to select the pins and the scan slots. Do the following:

   - Configure channels for the button electrodes using the drop-down menu.

     As seen in **Figure 15**, the button needs to be equally distributed between channel 0 and channel 1.

   - Configure pins for the electrodes using the drop-down menu.

   - Configure the scan slots using **Auto-assign slots** option or each sensor is allotted a scan slot based on the entered slot number. 

       The summary section in the **Scan configuration** tab shows 1 scan slots (for 2 sensors), with each channel scanned simultaneously in a single slot. This helps to perform parallel scanning and reduces the total scan time. To scan the sensors in same slot we need to keep both sense clock divider and number of sub-conversions to be same, with the values corresponding to the button with the highest Cp.

      **Note** See [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design Guide](https://www.cypress.com/an85951) for more details on Scan slot allotment rules.

   - Check the notice list for warning or errors.

   **Figure 15. Scan configuration tab**

   <img src="images/scan-configuration.png" alt="Figure 15"/>

10. Click **Save** to apply the settings.

</details>

<details><summary><b> Stage 2: Measure the Parasitic capacitance (Cp) </b></summary>

Use one of the following options to determine the Cp of the sensor:

   - [Option 1: Using BIST API in CAPSENSE&trade; middleware](#option-1-using-bist-api-in-capsense-middleware)

   - [Option 2: Using LCR meter](#option-2-using-lcr-meter)

   #### **Option 1: Using BIST API in CAPSENSE&trade; middleware**

   While using this procedure, ensure that you have enabled the **Enable self-test library** option in the CAPSENSE&trade; configurator. After you obtained the Cp value, you can disable this option.

   1. Estimate the Cp of the sensor electrode using the `Cy_CapSense_MeasureCapacitanceSensorElectrode()` function in firmware. The measured capacitance value is in femtofarad (fF).
   
   2. Program the board in Debug mode.

      In the IDE, use the **\<Application Name> Debug (KitProg3)** configuration in the **Quick Panel**.

      For more details, see the "Program and Debug" section in the Eclipse IDE for ModusToolbox&trade; user guide: *{ModusToolbox install directory}/ide_{version}/docs/mt_ide_user_guide.pdf*.

   3. Place a breakpoint after the capacitance measurement.

   4. In the **Expressions** window, add the Cp measurement variables (**button0_cp**, **button0_cp_staus**, **button1_cp**, **button1_cp_status**).

      The status of the measurement can also be read through the return value of the function in the **Expressions** window.

   5. Click the **Resume** button (green arrow) to reach the breakpoint.

      Note that the function return value reads `CY_CAPSENSE_BIST_SUCCESS_E` and the measurement variables provide the capacitance value of the sensor elements in **femtofarad** as shown in **Figure 5**.

   6. Click the **Terminate** button (red box) to exit Debug mode.

      **Figure 16. Cp measurement using BIST**

      <img src="images/debug-cp-measure.png" alt="Figure 16" />

   #### **Option 2: Using LCR meter**

   Measure the Cp of the sensor electrode of the button using an LCR meter. The Cp should be measured between the sensor electrode (sensor pin) and the device ground.

   **Table 1. Cp values obtained for CY8CKIT-041S-MAX kit**

   | Kit     | Parasitic capacitance (C<sub>P</sub>) in pF 
   |:---------------------|:----------------------------------------|
   | CY8CKIT-041S-MAX (Pin P11.2) |          24  |
   | CY8CKIT-041S-MAX (Pin P0.3)  |          30  |

</details>

<details><summary><b>Stage 3: Calculate and set the Sense clock frequency and Init sub conversions</b></summary>

1. Calculate maximum sense clock frequencies using **Equation 1**

   **Equation 1. Maximum sense clock frequency**

   <img src="images/fsw-equation.png" alt="Equation 1" width="200"/>

   where,

   - Cp is the Parasitic capacitances of the sensor electrode. This value is obtained from **Stage 2**.

   - R<sub>SeriesTotal</sub> is the total series resistance, which includes the 525-ohm (for CTRLMUX mode) internal resistance, the external series resistance (in CY8CKIT-041S MAX, it is 2 kilo-ohm), and the trace resistance. Include the trace resistance if high-resistive material such as ITO or conductive ink is used. The external resistor is connected between the sensor pad and the device pin to reduce the radiated emission. ESD protection is built into the device.

2. The sense clock divider value, as given by **Equation 2**, is obtained by dividing HFCLK (48 MHz) by **Maximum sense clock frequency (kHz)** calculated and choosing the nearest ceiling sense clock divider option in the configurator.
      
   **Equation 2. Sense clock divider**

   ![Equation 2](images/scd-equation.png)


   **Table 2. Sense clock frequency settings for CY8CKIT-041S-MAX Kit from Cp**

   |Development Kit | Cp of Sensor electrode (pF)| R<sub>SeriesTotal</sub> (ohm) |  Maximum sense clock frequency (kHz)| Sense clock divider | 
   | --- | --- | --- | --- | --- |
   |CY8CKIT-041S-MAX (Pin P11.2)| 24 | 2.525k | 825 | 59 |
   |CY8CKIT-041S-MAX (Pin P0.3) | 30  | 2.525k | 660 | 73 |

   **Note** 
   - If you are explicitly using the PRS or SSCx clock source to lower electromagnetic interference, ensure that you select the sense clock frequency that meets the conditions mentioned in the [ModusToolbox&trade; CAPSENSE&trade; configurator guide](https://www.cypress.com/file/492896/download) in addition to the above conditions. PRS and SSCx techniques spread the frequency across a range.

   - Actual Sense clock frequency value is choosen such that the divider is divisible by 4, in order to have all the 4 scan phases for equal durations. 

   -  If you want to scan channel 0 and channel 1 in the same scan slot simultaneously, the Sense clock divider and the number of sub-conversion should be the same for both sensor elements. Use the values corresponding to the sensor with the highest Cp.

      **Table 3. Sense clock frequency settings for CY8CKIT-041S-MAX kit**

   |Development kit | Sense clock divider | 
   | --- | ---  |
   |CY8CKIT-041S-MAX (Pin P11.2)|  60 |
   |CY8CKIT-041S-MAX (Pin P0.3) |  76 |


3. The maximum frequency set should charge and discharge the sensor completely, which you can verify using an oscilloscope and an active probe. To view the charging and discharging waveforms of the sensor, probe at the sensors (or as close as possible to the sensors), and not at the pins or resistor. An example of proper and improper charging of the sensors is shown in **Figure 17** and **Figure 18** respectively. You can also use a passive probe which will add an additional parasitic capacitance of around 15pF and thus the tuning may be not optimal.

   
   **Figure 17. Proper charge cycle of a sensor**

   <img src="images/csdrm-waveform.png" alt="Figure 15" width="400"/>

   **Figure 18. Improper charge cycle of a sensor**

   <img src="images/csdrm-waveform_improper.png" alt="Figure 16" width="400"/>

   Set the calculated value in the CAPSENSE&trade; configurator using the steps given in **Step 8** in **Stage 1**, which ensures the maximum possible sense clock frequency (for good gain) while allowing the sensor capacitance to fully charge and discharge in each phase of the MSC CSD sensing method.

4. Calculate and set the **Number of init sub-conversions** using the below equation. 

   Note: **Equation 3** is considering the default values of Cmod=2.2nF, Base % = 0.5 (50%), Auto-calibration % = 0.85 (85%). If you intend to change any value, refer to the [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.cypress.com/an85951) to calculate the required number of init sub-conversions.

   **Equation 3: Number of init sub-conversions** 

   <img src="images/no-init-sub-conv.png" alt="Equation 3" width="200"/>

   where, 
   VDDA = 5 V
   Cs = Least self capacitance value out of the sensors in pF (obtained in **Stage 2**)

5. Program the board.

6. Fine tune the sense clock frequency

   1. Check the calibration pass/fail status from the return value of the function `Cy_CapSense_Enable()`. 

   2. Launch the CAPSENSE&trade; tuner to monitor the CAPSENSE&trade; data and for CAPSENSE&trade; parameter tuning.
   
      See the [CAPSENSE&trade; tuner guide](https://www.cypress.com/ModusToolboxCapsenseTuner) for step-by-step instructions on how to launch and use the CAPSENSE&trade; tuner in ModusToolbox&trade;.

   3. Ensure that the following condition is satisfied for the selected sense clock frequency:

      **Note:** Calibration may fail if the obtained rawcounts is not within the targetted range. 

      - The auto-calibrated reference CDAC value should be above (20/compensation CDAC divider). Verify this once the initial hardware parameters are loaded into the device.

      - Click **Button0** in the **Widget Explorer** to view the Reference CDAC value in the sensor parameters window.
      - Also, click each sensor element, for instance, **Button0_Sns0** in the **Widget Explorer** to view the Compensation CDAC in the sensor parameters window. 

      Refer to the [CAPSENSE&trade; design guide](https://www.cypress.com/an85951) for the recommended guidelines on valid CDAC range (with and without compenation) to result in calibration PASS across multiple boards due to board-to-board variations.


      **Figure 19. Widget Explorer - button 0**

      <img src="images/tuner-cdac-setting-b0.png" alt="Figure 19" width="600"/>


      **Figure 20. Widget Explorer - button 1**

      <img src="images/tuner-cdac-setting-b1.png" alt="Figure 20" width="600"/>


   4. If the above condition is not satified. Fine-tune the sense clock divider to bring the CDAC value within range.

      1. If the Reference CDAC value is not in the recommended range, increase or decrease the sense clock divider in the Widget hardware parameters window.

         **Note** From the raw count equation ( see [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.cypress.com/an85951)), it is evident that increasing the sense clock divider will decrease the reference CDAC value for a given calibration percent and vice versa.

      2. Click **To device** to apply the changes to the device as shown in **Figure 21**.

         **Figure 21. Apply changes to device**

         <img src="images/tuner-apply-settings.png" alt="Figure 21"/>
         
      3. Click each sensor element, for instance, **Button0** in the Widget explorer.

      4. Observe the Reference CDAC value in the **Sensing parameters** section of the Widget parameters window.

      5. Repeat steps 1 to 4 until you obtain Reference CDAC value is above (20/Compensation CDAC divider).

   5. If the CDAC value is still not in the required range based on fine tuning the sense clock divider then consider reducing the modulator clock frequency to 24 MHz. The sense clock frequency is dervied from modulator clock frequency. Thus the corresponding sense clock divider values needs to be updated.

   6. Actual Sense clock frequency value is choosen such that the divider is divisible by 4, in order to have all the 4 scan phases for equal durations.

   7. Capture the raw counts of each sensor  (as shown in **Figure 22**) and verify that they are approximately (+/- 5%) equal to 85% of the MaxCount. See [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.cypress.com/an85951) for the MaxCount equation.

      **Figure 22. Verifying raw count calibration level**

      <img src="images/tuner-graph-view.png" alt="Figure 22"/>

   **Note:** 

   As **Figure 19** and **Figure 20** shows, CDAC values are in the recommended range. You can leave the sense clock divider to the value as shown in **Step 2** of **Stage 3**.

</details>

<details> <summary><b>Stage 4: Use CAPSENSE&trade; tuner to fine tune for required SNR and refresh rate</b> </summary>


1. Update the number of sub-conversions.

   Do the following to update the number of sub-conversions:

   1. Update the number of sub-conversions (N<sub>sub</sub>) directly in the **Widget/Sensor parameters** tab of the CAPSENSE&trade; tuner.

   2. Increase or decrease the number of sub-conversions by 10 and load the parameters to the device. The signal level is directly proportional to number of sub-conversion 

   **Note:** The sense clock divider and the number of sub-conversions should be same for both the sensors scanned in the same slot. Use the values corresponding to the sensor with the highest Cp.

2. Measure SNR as mentioned in the [Operation](#operation) section. And tune until the minimum SNR of 5:1 and at least a signal count greater than 50 are achieved.

3. Skip this step if the following conditions are met:

      - Measured SNR from the previous stage is greater than 5:1.
      - Signal count is greater than 50.

   If your system is very noisy (counts >20), do the following to set enable fitlers. 

   1. Open **CAPSENSE&trade; configurator** from ModusToolbox&trade; quick panel and select the appropriate filter:

      **Figure 23. Filter settings in CAPSENSE&trade; configurator**

      <img src="images/advanced-filter-settings.png" alt="Figure 23"/>

      **Note:**
      - Add the filter based on the type of noise in your measurements. See [ModusToolbox&trade; CAPSENSE&trade; configurator guide](https://www.cypress.com/file/492896/download) for details.
      - The current example has SNR around 10:1; therefore, filters are not enabled.

   2. Reprogram the device to update filter settings.
 
### Measure refresh rate.

Refresh rate will impact overall power consumption and user experience of the device in CAPSENSE&trade; applications. You can measure the refresh rate by toggling one of the GPIOs in each sensor scan loop. Probing the GPIO (P10.4 on J3) on the Oscilloscope shows the refresh rate as shown in **Figure 24**.

**Figure 24. Probing GPIO for refresh rate** 

<img src="images/probed-refresh-rate.png" alt="Figure 24" width="400"/>

**Note:**
Refresh rate obtained here is with the CAPSENSE&trade; tuner closed, as CAPSENSE&trade; tuner is only used for the purpose of debugging and will not play a role in deciding the Refresh rate in the end application. Also BIST feature is disabled. BIST is used to measure the Cp of the sensor at the initial stage of tuning.

Refresh rate from **Figure 24** = 1 /340us = 2941 Hz

   **Note:** 

   - Total scan time is equal to the sum of initialization time and the scan time given by **Equation 4**.

      **Equation 4. Scan time**

      <img src="images/scantime-equation.png" alt="Equation 4" width="150"/>
   
   - Refresh rate is the reciprocal of sum of total scan time and procesing time.

If the Refresh rate meets your requirements, go to next step otherwise fine tune the number of sub conversions.

</details>

<details><summary><b> Stage 5: Use CAPSENSE&trade; tuner to tune threshold parameters </b></summary>

The software threshold is set for each widget based on the diff counts. Steps for setting the threshold for one of the widget is given below. 

1. Switch to the **Graph view** tab and select **Button1**.

2. Touch the sensor and monitor the touch signal in the **Sensor signal** graph as **Figure 25** shows. Place the metal finger at all possible positions and use the least signal for setting the software threshold. Also ensure to ground the metal finger.

   **Figure 25. Sensor signal when the sensor is touched**

   <img src="images/tuner-diff-signal.png" alt="Figure 25"/>

3. When the signal is measured, set the thresholds according to the following recommendations:

   - Finger threshold = 80 percent of signal

   - Noise threshold = 40 percent of signal

   - Negative noise threshold = 40 percent of signal

   - Hysteresis = 10 percent of signal

   - Debounce = 3

4. Set the threshold parameters in the **Widget/Sensor parameters** section of the CAPSENSE&trade; tuner:

   **Figure 26. Widget threshold parameters**

   <img src="images/tuner-threshold-settings.png" alt="Figure 26" width="400"/>

5. Apply the settings to the device and to the project by clicking **To device** and then **To Project** as **Figure 27** shows, and close the tuner. The change is updated in the *design.cycapsense* file and reflected in the CAPSENSE&trade; configurator.

   **Figure 27. Apply to project setting**

   <img src="images/tuner-apply-settings.png" alt="Figure 27"/>

6. Consider testing with metal finger with smaller sizes that should be rejected by the system to ensure that they do not reach the finger threshold. If your sensor is tuned correctly, you will observe the touch status go from 0 to 1 in the **Status** sub-window of the **Graph View** window as **Figure 28** shows. The successful tuning of the button is also indicated by the LED in the pioneer kit; the LED is turned ON when the finger touches the button and turned OFF when the finger is removed.

   **Figure 28. Sensor status in CAPSENSE&trade; tuner**

   <img src="images/tuner-status.png" alt="Figure 28"/>

7. Close the CAPSENSE&trade; tuner and launch **CAPSENSE&trade; configurator**. You should now see all the changes that you made in the CAPSENSE&trade; tuner reflected in the **CAPSENSE&trade; configurator**.


   **Table 4. Software tuning parameters obtained based on sense for CY8CKIT-041S-MAX** 
  
   |Parameter|	 CY8CKIT-041S-MAX (Pin P11.2)|CY8CKIT-041S-MAX (Pin P0.3)|
   |:--------|:------|:------|
   |Signal	| 80	| 60 |
   |Finger threshold 	| 64| 48 |
   |Noise threshold |32| 24|
   |Negative noise threshold	|32 | 24 |
   |Hysteresis	| 8 | 6|
   |ON debounce	|3| 3|
   |Low baseline reset	| 30| 30|


</details>

<br>

## Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For more details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.cypress.com/MTBEclipseIDEUserGuide).


## Design and implementation

The project contains two button widgets configured in CSD-RM sensing mode. See the [Tuning procedure](#tuning-procedure) section for step-by-step instructions to configure the other settings of the **CAPSENSE&trade; configurator**.

The project uses the [CAPSENSE&trade; middleware](https://github.com/Infineon/capsense) (see ModusToolbox&trade; user guide for more details on selecting a middleware). See [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.cypress.com/documentation/application-notes/an85951-psoc-4-and-psoc-6-mcu-capsense-design-guide) for more details on CAPSENSE&trade; features and usage.

The [ModusToolbox&trade; software](https://www.cypress.com/products/modustoolbox-software-environment) provides a GUI-based tuner application for debugging and tuning the CAPSENSE&trade; system. The *CAPSENSE&trade; tuner* application works with EZI2C and UART communication interfaces. This project has an SCB block configured in EZI2C mode to establish communication with the on-board KitProg, which in turn enables reading the CAPSENSE&trade; raw data by the CAPSENSE&trade; tuner. See [EZI2C - Peripheral settings](#resources-and-settings).

The CAPSENSE&trade; data structure that contains the CAPSENSE&trade; raw data is exposed to the CAPSENSE&trade; tuner by setting up the I2C communication data buffer with the CAPSENSE&trade; data structure. This enables the tuner to access the CAPSENSE&trade; raw data for tuning and debugging CAPSENSE&trade;.

The successful tuning of the button is indicated by an LED in the pioneer kit: the LED is turned ON when the finger touches the button and turned OFF when the finger is removed from the button.


### Steps to setup the VDDA supply voltage in device configurator

1. Open Device configurator from the Quick panel. 

2. Go to the **System** tab. Select the **Power** resource, and set the set the VDDA value under **Operating conditions** as shown in **Figure 29**. 

   **Figure 29. Setting the VDDA supply in system tab of device configurator**

   <img src="images/vdda-settings.png" alt="Figure 29"/> 

**Note**: [PSoC&trade; 4100S Max pioneer kit](https://www.cypress.com/documentation/development-kitsboards/psoc-4100s-max-pioneer-kit-cy8ckit-041s-max) has two onboard regulators 3.3V and 5V. To use 3.3V, place the jumper J10 at positions 2 and 3. See the Kit user guide for more details.


### Resources and settings

**Figure 30. EZI2C settings**

<img src="images/ezi2c-config.png" alt="Figure 30" width="600"/>

**Table 3. Application resources**

| Resource  |  Alias/Object     |    Purpose     |
| :------- | :------------    | :------------ |
| SCB (I2C) (PDL) | CYBSP_EZI2C          | EZI2C slave driver to communicate with CAPSENSE&trade; tuner |
| CAPSENSE&trade; | CYBSP_MSC0,CYBSP_MSC1 | CAPSENSE&trade; driver to interact with the MSC hardware and interface the CAPSENSE&trade; sensors |
| Digital pin | CYBSP_LED_BTN0,CYBSP_LED_BTN1 | To show the button operation|

</details> 

<br>

### Firmware flow

**Figure 31. Firmware flowchart**

<img src="images/firmware-flowchart.png" alt="Figure 31"/>

<br>

## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.cypress.com/AN79953) – Getting started with PSoC&trade; 4 <br> [AN85951](https://www.cypress.com/AN85951) – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide
Code examples | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub <br> [Using PSoC&trade; Creator](https://www.cypress.com/documentation/code-examples/psoc-345-code-examples)
Device documentation | [PSoC&trade; 4 datasheets](https://www.cypress.com/search/all/PSOC%204%20datasheets?sort_by=search_api_relevance&f%5B0%5D=meta_type%3Atechnical_documents) <br>[PSoC&trade; 4 technical reference manuals](https://www.cypress.com/search/all/PSoC%204%20Technical%20Reference%20Manual?sort_by=search_api_relevance&f%5B0%5D=meta_type%3Atechnical_documents)
Development kits | Visit www.cypress.com/microcontrollers-mcus-kits and use the options in the **Select your kit** section to filter kits by *Product family* or *Features*.
Libraries on GitHub  | [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware abstraction layer (HAL) library
Middleware on GitHub | [CAPSENSE&trade;](https://github.com/infineon/capsense) – CAPSENSE&trade; library and documents <br>
Tools | [Eclipse IDE for ModusToolbox&trade; software](https://www.cypress.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon&reg; MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices. <br> [PSoC&trade; Creator](https://www.cypress.com/products/psoc-creator-integrated-design-environment-ide) – IDE for PSoC&trade; and FM0+ MCU development

<br>

## Other resources

Cypress provides a wealth of data at www.cypress.com to help you select the right device, and quickly and effectively integrate it into your design.

## Document history

Document title: *CE231078* - *PSoC&trade 4: MSC CAPSENSE&trade; CSD button tuning*

| Version | Description of change |
| ------- | --------------------- |
| 1.0.0   | New code example. <br /> This version is not backward compatible with ModusToolbox&trade; software v2.1.     |
| 2.0.0   | Code example is updated for ModusToolbox&trade; software v2.4. <br /> This version is not backward compatible with ModusToolbox&trade; software v2.3 or older version    |

------

All other trademarks or registered trademarks referenced herein are the property of their respective owners.

![banner](images/ifx-cy-banner.png)


---------------------------------------------------------------------

© Cypress Semiconductor Corporation, 2021. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br>
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br>
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit cypress.com. Other names and brands may be claimed as property of their respective owners.
