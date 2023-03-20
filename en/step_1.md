Go to the Inspector window for the 'Ball' and click on the **Add Component** button. 

Create a new script called `PlayerController`.

Open the script and enter the code below:

--- code ---
---
language: cs 
filename: PlayerController.cs 
line_numbers: true 
line_number_start: 1 
line_highlights: 
---

using System.Collections; 
using System.Collections.Generic; 
using UnityEngine;

public class PlayerController : MonoBehaviour { 
    public Transform cameraTransform; 
    public string forwardKey; 
    public string leftKey; 
    public string backwardKey; 
    public string rightKey; 
    Rigidbody rb;

// Start is called before the first frame update
void Start()
{
    rb = this.GetComponent<Rigidbody>();
    rb.transform.forward = cameraTransform.forward;
}

// FixedUpdate is called once per fixed frame-rate frame
void FixedUpdate()
{
    // Calculates cameraTransform.forward without the y value so the ball doesn't move up and down on the Y axis
    Vector3 forward = new Vector3(cameraTransform.forward.x, 0, cameraTransform.forward.z).normalized;
    Vector3 right = Quaternion.AngleAxis(90, Vector3.up) * forward;
    Vector3 left = -right;
    Vector3 backward = -forward;

    if (Input.GetKey(forwardKey))
    {
        rb.AddForce(forward * 5f);
    }

    if (Input.GetKey(rightKey))
    {
        rb.AddForce(right * 5f);
    }

    if (Input.GetKey(backwardKey))
    {
        rb.AddForce(backward * 5f);
    }

    if (Input.GetKey(leftKey))
    {
        rb.AddForce(left * 5f);
    }
}
}

--- /code ---

**Save** your code and return to Unity.

+ Select the 'Player1' GameObject to view the 'Inspector' options.

+ Drag the 'Main Camera' game object to the 'Camera Transform' variable in the 'Inspector'. 

+ Set the 'Forward Key', 'Left Key', 'Backward Key', and 'Right Key' to the lowercase letters that you want to use to control Player1. We used 'w', 'a', 's' and 'd'.

![The inspector for Player1 showing the PlayerController script with Camera Transform set to Main Camera and four key variables set to lowercase w, a, s and d.](images/player1-settings.png)

**Tip:** The letters for the keys need to be in lower case. 
