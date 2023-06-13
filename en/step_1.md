Go to the Inspector window for the sphere and click on the **Add Component** button. Add the `BallController` script component. 

--- collapse ---

---
title: Don't have a BallController script?
---

In the **Add Component** box, press <kbd>Enter</kbd> **twice** to create a new `BallController` script.

Go to the Project window. The new script will be saved in the Assets folder.

Drag the new script to the Scripts folder to organise your files.

Open the new script in your script editor. 

--- code ---
---
language: cs
filename: BallController.cs
line_numbers: true
line_number_start: 
line_highlights: 
---
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BallController : MonoBehaviour
{
    private Rigidbody rb;
    public Transform cameraTransform;
    public string upKey;
    public string leftKey;
    public string downKey;
    public string rightKey;

    // Start is called before the first frame update
    void Start()
    {
        rb = GetComponent<Rigidbody>();
        rb.transform.forward = cameraTransform.forward;
    }

    // FixedUpdate is called once per frame
    void FixedUpdate()
    {
        Vector3 forward = new Vector3(cameraTransform.forward.x, 0, cameraTransform.forward.z).normalized;
        Vector3 right = Quaternion.AngleAxis(90, Vector3.up) * forward;
        Vector3 left = -right;
        Vector3 backward = -forward;

        if (Input.GetKey(rightKey))
        {
            rb.AddForce(right * 5f);
        }

        if (Input.GetKey(leftKey))
        {
            rb.AddForce(left * 5f);
        }

        if (Input.GetKey(upKey))
        {
            rb.AddForce(forward * 10f);
        }

        if (Input.GetKey(downKey))
        {
            rb.AddForce(backward * 2f);
        }
    }
}
--- /code ---

**Save** your code and return to Unity.

--- /collapse ---

+ Select the Sphere GameObject to view the 'Inspector' options.

+ Drag the 'Main Camera' GameObject to the 'Camera Transform' variable in the Inspector. 

+ Set the 'Forward Key', 'Left Key', 'Backward Key', and 'Right Key' to the lower case letters that you want to use to control Player1. We used 'w', 'a', 's' and 'd'.

![The inspector for Player1 showing the PlayerController script with Camera Transform set to Main Camera and four key variables set to lower case w, a, s and d.](images/player1-settings.png)

**Tip:** The letters for the keys need to be in lower case. 
