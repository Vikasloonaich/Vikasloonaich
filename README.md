

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
    

    return 0;
}
