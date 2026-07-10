# Gesture Detection with Arduino
This project features a gesture detection device targeted towards ALS patients who have limited mobility and are unable to verbally communicate. The device can detect micro finger movements, with different movements corresponding to specific phrases which are displayed on a screen and read aloud through a speaker. This project stemmed from the following base project: [Link](https://docs.arduino.cc/tutorials/nano-33-ble-sense-rev2/get-started-with-machine-learning/), which required gripping the entire Arduino board while doing big hand movements. I modified this base project to utilise flex sensors attatched to the fingers in order for the algorithm to detect micro movements, linked gestures to the corresponding phrases, and added the display screen and speaker for patients to effectively communicate. 

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Gabrielle L | ISF | Biomedical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

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
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}https://www.amazon.com/Arduino-Nano-Sense-headers-ABX00070/dp/B0BQHZ88WD/
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Nano 33 BLE Sense | Tracks the gestures and runs the algorithm to process data | $39.7 USD | [Link](https://a.co/d/0b4ZIPly) |
| Micro USB | To connect the Arduino board to your device | $7.34 USD | [Link](https://www.amazon.com/Amazon-Basics-Charging-Transfer-Gold-Plated/dp/B07232M876/) |
| Electronics Kit | Provides neccessary hardware | $14 USD | [Link](https://www.amazon.com/Smraza-Electronics-Potentiometer-tie-Points-Breadboard/dp/B0B62RL725/r) |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
