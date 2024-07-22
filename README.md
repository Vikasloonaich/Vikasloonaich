#include <iostream>
#include <chrono>
#include <thread>

// Constants
const int GRAVITY = 1;   // Acceleration due to gravity
const int JUMP_FORCE = 10;  // Initial jump force

class Player {
private:
    int x, y;  // Player position
    int velocity;  // Vertical velocity
    bool isJumping;  // Flag to track if the player is jumping

public:
    Player(int startX, int startY) : x(startX), y(startY), velocity(0), isJumping(false) {}

    void jump() {
        if (!isJumping) {
            velocity = JUMP_FORCE;
            isJumping = true;
        }
    }

    void applyGravity() {
        if (y > 0) {  // Ground level assumption (y=0)
            velocity -= GRAVITY;
            y -= velocity;
        }

        if (y <= 0) {  // Check if player has landed
            y = 0;
            velocity = 0;
            isJumping = false;
        }
    }

    void moveLeft() {
        x--;
    }

    void moveRight() {
        x++;
    }

    void draw() {
        std::cout << "Player position: (" << x << ", " << y << ")\n";
    }
};

int main() {
    Player player(10, 0);  // Initial position (10, 0)

    char input;
    bool isRunning = true;

    while (isRunning) {
        // Simulate game loop, handling player input
        std::cout << "Enter command (j=jump, l=left, r=right, q=quit): ";
        std::cin >> input;

        switch (input) {
            case 'j':
                player.jump();
                break;
            case 'l':
                player.moveLeft();
                break;
            case 'r':
                player.moveRight();
                break;
            case 'q':
                isRunning = false;
                break;
            default:
                std::cout << "Invalid command!\n";
                break;
        }

        // Simulate gravity
        player.applyGravity();

        // Draw player position
        player.draw();

        // Pause briefly (simulate frame rate)
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }

    return 0;
}
