# Gesture Detection with Arduino
This project features a gesture detection device targeted towards ALS patients who have limited mobility and are unable to verbally communicate. The device can detect micro finger movements, with different movements corresponding to specific phrases which are displayed on a screen and read aloud through a speaker. This project stemmed from the following base project: [Link](https://docs.arduino.cc/tutorials/nano-33-ble-sense-rev2/get-started-with-machine-learning/), which required gripping the entire Arduino board while doing big hand movements. I modified this base project to utilise flex sensors attatched to the fingers in order for the algorithm to detect micro movements, linked gestures to the corresponding phrases, and added the display screen and speaker for patients to effectively communicate. 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Gabrielle L | ISF | Biomedical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)

  
# Final Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>



(I'm gonna make another video when I finish all the modifications I wanted to add after the program)

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE


# Third Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/V_1O0kNGWys?si=VWeheK56ym9BH6a2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

**Modifications**
- Flex sensors: Completed the wiring of the flex sensors, recollected data of the new gestures, updatated the algorithm code to support 8 columns of data (the two new columns being the two flex sensors)
   - ALS patients have limited mobility but often still have slight movement in their fingers and wrists, the flex sensors can detect extremely subtle small movements and finger twitches
- Made the gestures correspond to specific phrases
   - Allows for the ALS patients to be able to communicate with their families and doctors
 
**Challenges I faced**  
- Wiring the flex sensors: The pins were short and weirdly shaped, leading to loose connections
   - To overcome this, I tried many different solutions, including:
   - Taping the pins and wires together using electrical tape, but because the pins were so small, it was hard to securely connect it with the tape, and the sensors were therefore unable to be detected
   - Using bobby pins to make the connections more secure, but the bobby pins themselves kept moving around
   - Purchasing adapters so the flex sensors can securely attatch to the breadboard, but I was unable to find the official adapter and the alternatives I purchased failed
   - Finally, I decided to make a permanent and secure connection by soldering the pins and wires together
 
**Next Steps**
- Connecting the OLED display screen and speaker
- Writing up the code for the two add ons


# Second Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/kgX9mb2ExEQ?si=B0Hw3EbwrpzRuEkY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

**Technical details**
- Exported the algorithm onto the Arduino board for live gesture recognition
- Tested the algorithm and made sure it was accurately detecting all the gestures
- Base project completed
- Prints the algorithm's confidence level on which movement it detects, 1 being 100% confident

**What has been surprising about the project so far**
- I was suprised by how easily transferable the machine learning code and model structures are across different platforms
- I was also shocked that the algorithm was able to so highly accurately detect the gestures I was doing, with the confidence level being 100% most of the time

**Previous challenges I faced**
- Arduino TensorFlow Lite library was archived and no longer supported by the Arduino IDE
   - To overcome this, I had to manually find the files, and received help from supervisors who were able to provide me with the neccessary code
- Algorithm stopped working and started completely guessing the gestures, predicting 50/50 confidence levels for both gestures despite what movement was actually being done
   - To overcome this, I found that there was a mismatch between the alogrithm training enviorment and the hardware. I resolved this by fixing the calibration mapping and normalising the live input data in the Arduino code

**What needs to be completed before your final milestone**
- Changing to using flex sensors attatched to the fingers in order to detect micro movements
- Updating the data to include gestures based on the movement of ALS patients
- Updating the algorithm to fit the flex sensors
- Making different gestures correspond to specific phrases
- Adding a screen displaying these phrases, as well as a speaker which reads the phrases out loud


# First Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/fzMGlm0GncQ?si=rIums7j7ZTaQL_my" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

**Technical progress you’ve made so far**
- Setting up the base hardware and code
- Data collection: The same gestures were repeated 10+ times to provide the algorithm with more examples of the gesture, ensuring higher accuracy
- Built and trained the algorithm: Tensorflow was used to parse the data, and the algorithm was able to learn the patterns of each gesture
- Tested the algorithm to ensure accuracy

**Challenges you’re facing and solving in your future milestones**
- I had issues downloading Tensorflow onto my computer
   - In the end I was able to figure out the problem, which included differences in my Python version, as well as a lack of storage space on my computer
- Difficulties uploading the data, the files not being the right format
   - To overcome this, I used another platform, Visual Studio Code, to store and download my data

**What your plan is to complete your project**
- Export the trained algorithm and deploy it to Arduino
- Add more gestures and link them to the specific phrases
- Work on modifications: Flex sensors, screen display, speaker


# Schematics 
![Schematics](/Gabby_BluestampPortfolio/assets/schematic.jpg)


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
#include "Arduino_BMI270_BMM150.h"
#include <TensorFlowLite.h>
#include <tensorflow/lite/micro/all_ops_resolver.h>
#include <tensorflow/lite/micro/micro_interpreter.h>
#include <tensorflow/lite/schema/schema_generated.h>

#include "model.h"
#include "Phrases.h"

const int FLEX_1_PIN = A0; 
const int FLEX_2_PIN = A1; 

const int numSamples = 15;
const int NUM_FEATURES = 8;             
int samplesRead = 0; 

tflite::AllOpsResolver tflOpsResolver;
const tflite::Model* tflModel = nullptr;
tflite::MicroInterpreter* tflInterpreter = nullptr;
TfLiteTensor* tflInputTensor = nullptr;
TfLiteTensor* tflOutputTensor = nullptr;

constexpr int tensorArenaSize = 12 * 1024; 
byte tensorArena[tensorArenaSize] __attribute__((aligned(16)));

const char* GESTURES[] = {
  "Idle",
  "2nd_finger_down",
  "3rd_finger_down",
  "both_fingers_down"
};
#define NUM_GESTURES (sizeof(GESTURES) / sizeof(GESTURES[0]))

void setup() {
  Serial.begin(9600);
  while (!Serial); 

  Serial.println("--- Bare Minimum + Phrases Test ---");

  if (!IMU.begin()) {
    Serial.println("Failed to initialize IMU!");
    while (1);
  }
  
  pinMode(FLEX_1_PIN, INPUT);
  pinMode(FLEX_2_PIN, INPUT);

  tflModel = tflite::GetModel(model);
  tflInterpreter = new tflite::MicroInterpreter(
    tflModel, tflOpsResolver, tensorArena, tensorArenaSize
  );

  tflInterpreter->AllocateTensors();
  tflInputTensor = tflInterpreter->input(0);
  tflOutputTensor = tflInterpreter->output(0);

  Serial.println("Setup Complete. Streaming live predictions and phrases...");
}

void loop() {
  float aX = 0, aY = 0, aZ = 0;
  float gX = 0, gY = 0, gZ = 0;

  if (IMU.accelerationAvailable()) {
    IMU.readAcceleration(aX, aY, aZ);
  }
  if (IMU.gyroscopeAvailable()) {
    IMU.readGyroscope(gX, gY, gZ);
  }
  
  float flex1 = analogRead(FLEX_1_PIN);
  float flex2 = analogRead(FLEX_2_PIN);

  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 0] = (aX + 4.0) / 8.0;
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 1] = (aY + 4.0) / 8.0;
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 2] = (aZ + 4.0) / 8.0;
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 3] = (gX + 2000.0) / 4000.0;
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 4] = (gY + 2000.0) / 4000.0;
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 5] = (gZ + 2000.0) / 4000.0;
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 6] = flex1 / 1023.0; 
  tflInputTensor->data.f[samplesRead * NUM_FEATURES + 7] = flex2 / 1023.0; 

  samplesRead++;

  if (samplesRead == numSamples) {
    tflInterpreter->Invoke();

    Serial.println("\n=====================================");
    
    int bestGestureIndex = 0;
    float maxConfidence = 0.0;

    for (int i = 0; i < NUM_GESTURES; i++) {
      float confidence = tflOutputTensor->data.f[i] * 100.0;
      Serial.print(GESTURES[i]);
      Serial.print(": ");
      Serial.print(confidence, 1);
      Serial.println("%");

      if (confidence > maxConfidence) {
        maxConfidence = confidence;
        bestGestureIndex = i;
      }
    }
    
    String assignedPhrase = getPhraseForGesture(bestGestureIndex);

    Serial.print("\n>>> DETECTED: ");
    Serial.println(GESTURES[bestGestureIndex]);
    Serial.print(">>> PHRASE:   ");
    Serial.println(assignedPhrase);
    Serial.println("=====================================");
    
    samplesRead = 0; // Reset sample pointer
    delay(1000);     // 1-second delay so you can easily read the terminal updates
  }
  delay(20); // Tiny pause to space out the 15 window frames cleanly
}
```

For Phrases:
```c++
#ifndef PHRASES_H
#define PHRASES_H

#include <Arduino.h>

inline String getPhraseForGesture(int gestureIndex) {
  switch(gestureIndex) {
    case 0:
      return "System is resting.";
    case 1:
      return "Hello!";
    case 2:
      return "Thank you";
    case 3:
      return "Goodbye";
    default:
      return "Unknown gesture.";
  }
}

#endif
```

# Bill of Materials
| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Nano 33 BLE Sense | Tracks the gestures and runs the algorithm to process data | $39.7 USD | [Link](https://a.co/d/0b4ZIPly) |
| Micro USB | To connect the Arduino board to your device | $7.34 USD | [Link](https://www.amazon.com/Amazon-Basics-Charging-Transfer-Gold-Plated/dp/B07232M876/) |
| Electronics Kit | Provides neccessary hardware | $14 USD | [Link](https://www.amazon.com/Smraza-Electronics-Potentiometer-tie-Points-Breadboard/dp/B0B62RL725/r) |
| 2.2" Flexible Sensor | Measures finger bending angles and senses gestures | $15.95 USD | [Link](https://a.co/d/04WPG198) |
| 2.42-inch 128x64 I2C OLED Display Module | Provides a visual display for live text outputs | $15.99 USD | [Link](https://a.co/d/01P6DQxX) |
| DFRobot Gravity: Digital Speaker Module FIT0449 | Converts text output into live audio phrases and voice assistance | $26.90 USD | [Link](https://www.dfrobot.com/product-2234.html) |


# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Base Project Tutorial:](https://docs.arduino.cc/tutorials/nano-33-ble-sense-rev2/get-started-with-machine-learning/)
- [Google Colab For Base Project](https://colab.research.google.com/)
- [Google Colab With Modifications](https://colab.research.google.com/drive/1V5pKz0cHDzcEqBW0U2JlFXTMre7V5yi3?usp=sharing)

