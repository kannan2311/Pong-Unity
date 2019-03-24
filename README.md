ABSTRACT 
In Today’s World everything is made as application. From the Born to the Death everything can be done easily by using Internet, Software Application, Websites, Smartphones and so on. In our day-to-day life, Scientist and Researcher are struggling more to make this technology user-friendly to everyone. The Devices are actually more user-friendly in some functions, but they are working to make everything user-friendly to everyone. We can see a new born child who doesn’t know any language are using smartphones are often.  They will observe how other’s using smartphones and they will do when then have one. This is user-friendly.  Apart from using smartphone for our Work, Education, Knowledge we all are using it for Entertainment purpose also. The Children will play game, Adult can play games hear songs, Old watch News, TV Shows.

INTRODUCTION
Pong is a game which some of us might played in our Childhood. This game will contain a Ball and a Brick in other words plate. When we start the game, the ball will start to move in random direction, we have to move the Brick/Plate in the place where the ball is going to hit the boundary. The thing is we have to maintain a ball to keep moving without touching the boundary. If the ball touches the boundary, it will be considered as We Lost. The time how long we are maintaining the ball without touching the edge is the score. The Pong we played will have only one Ball and One Plate but the Pong I developed will have One Ball and Two Plate. This can be played as a Single-Player as-well as Multi-Player. I have incorporated a Blue plain screen as Background. The Ball and Plate will be in White Colour so that it will be visible clearly in Blue Background.


METHODOLOGY
	ALGORITHM
1.	Create a Background
2.	Create a Ball, Plate and Place it in the Game
3.	Create a C# script for Game Component, Ball, Plate
4.	Adjust the Ball, Plate position
5.	Type C# code for moving the Objects
6.	Type C# code for object reflection.
CODE
GAME COMPONENT
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GameManager : MonoBehaviour{

    public Ball ball;
    public Paddle paddle;

    public static Vector2 bottomLeft;
    public static Vector2 topRight;

    // Use this for initialization
    void Start(){

        // Convert screen's pixel coordinate into game's coordinate
        bottomLeft = Camera.main.ScreenToWorldPoint (new Vector2(0, 0));
        topRight = Camera.main.ScreenToWorldPoint (new Vector2(Screen.width, Screen.height));

        //Create Ball 
        Instantiate(ball);

        // Create Two paddles
        Paddle paddle1 = Instantiate(paddle) as Paddle;
        Paddle paddle2 = Instantiate(paddle) as Paddle;
        paddle1.Init (true); // right paddle
        paddle2.Init (false); // left paddle
    }
}
BALL
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Ball : MonoBehaviour{

    [SerializeField]
    float speed;

    float radius;
    Vector2 direction;


    // Start is called before the first frame update
    void Start() {
        direction = Vector2.one.normalized; // direction is (1,1) normalized
        radius = transform.localScale.x / 2; //half the width
    }

    // Update is called once per frame
    void Update()    {
        transform.Translate(direction * speed * Time.deltaTime);

        // Bounce off top and bottom
        if (transform.position.y < GameManager.bottomLeft.y + radius && direction.y < 0)        {
            direction.y = -direction.y;
        }
        if (transform.position.y > GameManager.topRight.y - radius && direction.y > 0)        {
            direction.y = -direction.y;
        }

        // Game over
        if (transform.position.x < GameManager.bottomLeft.x + radius && direction.x < 0)       {
            Debug.Log("Right player wins !!");

        }
        if (transform.position.x > GameManager.bottomLeft.x - radius && direction.x > 0)        {
            Debug.Log("Left player wins !!");

        }
    }

        void OnTriggerEnter2D(Collider2D other)       {
            if (other.tag == "Paddle")           {
                bool isRight = other.GetComponent<Paddle> ().isRight;

                // If hitting right paddle and moving right, flip direction
                if (isRight == true && direction.x > 0)              {
                    direction.x = -direction.x;
                }
                //If hitting left paddle and moving right, flip direction
                if (isRight == false && direction.x < 0)               {
                    direction.x = -direction.x;
                }
            }
        }

    
}
PADDLE
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Paddle : MonoBehaviour{

    [SerializeField]
    float speed;
    float height;

    string input;
    public bool isRight;

    // Use this for initialization
    void Start(){
        height = transform.localScale.y; 
    }

    public void Init(bool isRightPaddle) {

        isRight = isRightPaddle;

        Vector2 pos = Vector2.zero;

        if (isRightPaddle)  {
            // Place paddle on the right of screen
            pos = new Vector2(GameManager.topRight.x, 0);
            pos -= Vector2.right * transform.localScale.x; //Move a bit to the left  

            input = "PaddleRight";
        }    else   {
            // Place paddle on the left of screen
            pos = new Vector2(GameManager.bottomLeft.x, 0);
            pos += Vector2.right * transform.localScale.x; //Move a bit to the Right

            input = "PaddleLeft";
        }

        // Update this paddle's position
        transform.position = pos;

        transform.name = input;
    }
    // Update is called once per frame
    void Update()    {
        //Now let's move the paddle!

        //GetAxis is a number between -1 to 1 (-1 for down, 1 for up)
float move = Input.GetAxis(input) * Time.deltaTime * speed;

//Restrict paddle movement
//If paddle is too low and user is continuing to move down, stop
if (transform.position.y < GameManager.bottomLeft.y + height / 2 && move < 0)        {
move = 0;
}
//If paddle is too low and user is continuing to move up, stop
if (transform.position.y > GameManager.topRight.y - height / 2 && move > 0)        {
move = 0;
}
transform.Translate(move * Vector2.up);

}
}
API 

 

RESULT
The Right Paddle will be controlled by the Player 1 and Left Paddle will be controlled by Player 2.  If Player 1 missed the ball He considered to be Lost and the Message “Left Player Wins !!” will be displayed. If Player 2 missed the ball, He considered to be Lost and the Message “Right Player Wins !!” will be displayed.

 

CONCLUSION
I have used Unity 2018.3.0 for developing this Game. This is my first experience with unity before this I haven’t used Unity. This is new and quite interesting experience. 

