```
#include "MicroBit.h"

MicroBit uBit; // The MicroBit object
const int16_t MAX_LENGTH = 7; // The length of the snake

// The length of the snake is MAX_LENGTH, i.e., from [0] to [MAX_LENGTH-1]. 
// The last position (i.e., [MAX_LENGTH]) holds the 
// previous position of the tail in order to erase it.

int16_t snake_x[MAX_LENGTH + 1]; 
// snake_x[0] is the x position of the head of the snake 
int16_t snake_y[MAX_LENGTH + 1]; 
// snake_y[0] is the y position of the head of the snake

// Initialise the arrays of the coordinates, so that 
// the head of the snake is in position (new_x_head, new_y_head) 
// and the remaining co-ordinates are set to -1.
void initialize_snake(int16_t new_x_head, int16_t new_y_head)
{
    int16_t i;
    snake_x[0] = new_x_head;
    snake_y[0] = new_y_head;

    for (i=1; i<MAX_LENGTH+1; i++)
    {
        snake_x[i] = -1;
        snake_y[i] = -1;      
    }
}

// Move the snake. Its head (element [0]) moves to the
// new coordinates (new_x_head, new_y_head)
// while element i moves to the co-ordinates that 
// element i-1 used to occupy.
void shift_snake(int16_t new_x_head, int16_t new_y_head)
{
    int16_t i;
    for (i=MAX_LENGTH; i>0; i--)
    {
        snake_x[i] = snake_x[i-1];
        snake_y[i] = snake_y[i-1];
    }
    snake_x[0] = new_x_head;
    snake_y[0] = new_y_head;
}

// Turn on element [0] (the head) and turn off element [MAX_LENGTH],
// where the tail (the last element of the snake) used to be in the previous step.
void display_snake()
{
    // Move the head forward
    if (snake_x[0]>=0 && snake_y[0]>=0)
        uBit.display.image.setPixelValue(snake_x[0], snake_y[0], 255);

    // Erase the tail
    if (snake_x[MAX_LENGTH]>=0 && snake_y[MAX_LENGTH]>=0)
        uBit.display.image.setPixelValue(snake_x[MAX_LENGTH], snake_y[MAX_LENGTH], 0);
}

int main()
{   
    int16_t x = 0; // The x co-ordinate
    int16_t y = 0; // The y co-ordinate

    // Initialise the micro:bit
    uBit.init();
    // Reveal the head of the snake at the top-left corner of the 5x5 display
    initialize_snake(x, y);

    while (1)
    {
        // Print the snake
        display_snake();
        // Wait for 100 ms
        uBit.sleep(100);

        // Consider the edge conditions, i.e., (4,0), (4,4), (0,4), (0,0)
        // and update the x and y co-ordinates accordingly,
        // so that the head of the snake changes direction when it reaches 
        // a corner of the 5x5 display.
        if (x < 4 && y == 0) // The head moves from the left to the right of the top row
            x++;
        else
        {
            if (x == 4 && y < 4) // The head moves from the top to the bottom of the right-most column
                y++;
            else
            {
                if (x > 0 && y == 4) // The head moves from the right to the left of the bottom row
                    x--;
                else
                {
                    if (x == 0 && y > 0) // The head moves from the bottom to the top of the left-most column
                        y--;
                }
            }
        }

        // Calculate the position of each pixel of the snake,
        // now that the position of its head is known.
        shift_snake(x, y);
    }
}
```

![[Pasted image 20241209024425.png]]
![[Pasted image 20241209024602.png]]
![[Pasted image 20241209024745.png]]
![[Pasted image 20241209025005.png]]

