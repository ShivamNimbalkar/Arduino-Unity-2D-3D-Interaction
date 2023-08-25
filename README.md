# Arduino Unity 2D/3D Interaction

This Unity project seamlessly integrates Arduino hardware with both 2D and 3D environments to create an interactive gaming experience. By using an Arduino Uno, a few jumper wires, and a membrane keyboard as a touch button, this project enables you to control in-game actions using real-world inputs. When a key is pressed on the membrane keyboard, a corresponding serial message is sent to the Unity console, allowing for direct interaction with Arduino-controlled devices.

The successful connection between Arduino and Unity is achieved through the [Ardity asset](https://ardity.dwilches.com/), which can be downloaded from the provided link.

## Features

- **Arduino Integration:** Use Arduino Uno and a membrane keyboard as a touch button to trigger in-game events.

- **Serial Communication:** Receive serial messages in Unity, enabling real-time interaction with Arduino-controlled hardware.

- **2D and 3D Environments:** This project offers compatibility with both 2D and 3D Unity environments, providing flexibility for different types of games and simulations.

- **Gameplay Element:** The project includes a 2D scene with a falling game object (square) that responds to keyboard inputs from the Arduino. When the designated key is pressed, the game logic executes a series of if statements to determine if the object should be destroyed, awarding points to the player. If the player fails to act in time, the object is automatically removed from the game at a specific y-axis location.

## Getting Started

To get started with this project, follow these steps:

1. **Hardware Setup:** Connect your Arduino Uno and the membrane keyboard to your computer using USB cables and jumper wires as per your specific hardware requirements.

2. **Ardity Installation:** Download and import the Ardity asset into your Unity project from [this link](https://ardity.dwilches.com/). Follow the installation instructions provided on the Ardity website to establish a successful connection between Arduino and Unity.

3. **Open the Project:** Open the Unity project included in this repository.

4. **Scene Setup:** Examine the 2D scene provided, which contains a falling game object (square). Customize this scene or replace it with your own game elements as needed.

5. **Arduino Configuration:** Modify the Arduino code to map key presses on the membrane keyboard to specific serial messages that Unity can understand and act upon.

6. **Unity Interaction:** Implement and customize the Unity scripts responsible for detecting serial messages and executing game logic based on user input from the Arduino.

7. **Testing:** Run the Unity project and test the interaction between the Arduino hardware and the game object. Ensure that pressing the designated key on the membrane keyboard triggers the desired in-game actions.

## Usage

This project serves as a foundation for creating interactive Unity experiences that incorporate Arduino hardware. You can extend and customize it to suit your specific gaming or simulation needs.
#Code for MyListener.cs
```
/**
 * Ardity (Serial Communication for Arduino + Unity)
 * Author: Daniel Wilches <dwilches@gmail.com>
 * Modifications for InterfaceLab 2020 to move a cube
 *  
 * This work is released under the Creative Commons Attributions license.
 * https://creativecommons.org/licenses/by/2.0/
 */
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class MyListener : MonoBehaviour
{
    [SerializeField]
    public GameObject objectToDestroy;
    public float targetLocation;
    void Start() // Start is called before the first frame update
    {

    }
    void Update() // Update is called once per frame
    {
        Debug.Log("Target Location: " + targetLocation);
        Debug.Log("Square Location: " + objectToDestroy.transform.position.y);
    }
    void OnMessageArrived(string msg)
    {

        Debug.Log("Buton Pressed: " + msg);
        if (msg == "1")
        {
            float lowerLimit = 50; // Replace with your lower limit
            float upperLimit = 60; // Replace with your upper limit

            if (objectToDestroy.transform.position.y >= lowerLimit && objectToDestroy.transform.position.y <= upperLimit)
            {
                Debug.Log("Objet about to kill at" + objectToDestroy.transform.position.y);
                Destroy(objectToDestroy);
                Debug.Log("Objetkilled at" + objectToDestroy.transform.position.y);
            }
            else
            {
                // Code to execute when the condition is not met
                Debug.Log("Object not destroyed because it's not within the specified range.");
            }
            else if (objectToDestroy.transform.position.y < -10)
            {
                // Code to automatically destroy the object when it falls below -10
                Debug.Log("Object automatically destroyed because it fell below -10 at " + objectToDestroy.transform.position.y);
                Destroy(objectToDestroy);
            }
        }



    }
    // Invoked when a connect/disconnect event occurs. The parameter 'success'
    // will be 'true' upon connection, and 'false' upon disconnection or
    // failure to connect.
    void OnConnectionEvent(bool success)
    {
        Debug.Log(success ? "Device connected" : "Device disconnected");
    }
}
```

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

We want to express our gratitude to the creators of the Ardity asset for facilitating seamless communication between Arduino and Unity.

## Support

If you encounter any issues or have questions about this project, please feel free to [reach out to us](https://github.com/yourusername/your-repo-name/issues) through the project's GitHub repository.

---

Thank you for choosing our Arduino Unity 2D/3D Interaction project. We hope it inspires you to create exciting and innovative interactive experiences. Enjoy gaming with a touch of the real world!
