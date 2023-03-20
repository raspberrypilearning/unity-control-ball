Go to the Inspector window for the 'Ball' and click on the **Add Component** button. 

Create a new script called `BallController`.

Open the script and enter the code below:

--- code ---
---
language: cs
filename: BallController.cs
line_numbers: true
line_number_start: 1
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BallController : MonoBehaviour
{
   private Rigidbody rb;
   public Transform cameraTransform;

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
       Vector3 right =  Quaternion.AngleAxis(90, Vector3.up) * forward;
       Vector3 left = -right;
       Vector3 backward = -forward;

       if (Input.GetKey("d"))
       {
           rb.AddForce(right * 5f);
       }

       if (Input.GetKey("a"))
       {
           rb.AddForce(left * 5f);
       }

       if (Input.GetKey("w"))
       {
          rb.AddForce(forward * 10f);
       }

       if (Input.GetKey("s"))
       {
          rb.AddForce(backward * 2f);
       }

       if (Input.GetKeyDown("space"))
       {
          rb.AddForce(0f, 75f, 0f);
       }
   } 
}

--- /code ---

**Save** your code and return to Unity.

With the 'Ball' GameObject selected in the 'Hierarchy' window. Drag the 'Main Camera' GameObject onto the `Camera Transform` variable in the 'Inspector' window inside the script.
