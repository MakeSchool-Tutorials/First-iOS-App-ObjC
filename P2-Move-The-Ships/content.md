---
title: "Move The Ships"
slug: move-the-ships
---   

##Step 1: Time to make the ships move!

We are going to make the ships move in two different ways. One will move automatically, the other will move to where you tap.

First, let's set up the automatic moving. Therefore we need to create a new method. Make sure you create this new method outside of any existing method. A good spot would be right after the closing curly brace at the end of the init method (before the @end). Paste in this code to create the method:

```
//method gets called every frame on every of your scenes
- (void)update:(CCTime)delta
{
    //move the ship only in the x direction by a fixed amount every frame
    ship1.position = ccp( ship1.position.x + 100*delta, ship1.position.y );

    if (ship1.position.x > self.contentSize.width+32)
    {
        //if the ship reaches the edge of the screen, loop around
        ship1.position = ccp( -32, ship1.position.y);
    }
}
```

This method will get called every frame and move the ship automatically. Run the program and see what happens!

##Step 2: Tap Tap Tap

Now we need to tell Cocos2D that our scene will accept touch input from a player. Add these lines to the end of your init method (just before the closing curly braces):

```
//Allow player to interact with this scene
self.userInteractionEnabled = TRUE;
```

Now we will be able to receive touches. To respond to a touch when we receive one, we need to add another method. Place this method between the init and the update method:

```
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    // 'touches' will only contain one touch, because we aren't using multitouch
    UITouch *touch = [touches anyObject];

    // we want to know the location of our touch in this scene
    CGPoint touchLocation = [touch locationInNode:self];

    // move the ship animated to the touch position
    [ship2 runAction: [CCActionMoveTo actionWithDuration:1.f position:touchLocation]];
}
```

Tap on the screen to see what happens! If for some reason it doesn't work, here's a full copy of the code so you can double check to make sure you didn't make any mistakes:

```
- (id)init
{
    if (self = [super init])
    {
        //Initialize the ship sprite with a specific file, the ship image
        ship1 = [CCSprite spriteWithImageNamed: @"ship.png"];

        //Set the ship's position. (0,0) is at the bottom left
        ship1.position = ccp( 50, 200 );

        //Initialize the other sprite
        ship2 = [CCSprite spriteWithImageNamed: @"ship.png"];

        //Set the other ship's position
        ship2.position = ccp( 100, 50 );

        //Add the ships to the game
        [self addChild:ship1];
        [self addChild:ship2];

        //Allow player to interact with this scene
        self.userInteractionEnabled = TRUE;
    }

    return self;
}

- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    // 'touches' will only contain one touch, because we aren't using multitouch
    UITouch *touch = [touches anyObject];

    // we want to know the location of our touch in this scene
    CGPoint touchLocation = [touch locationInNode:self];

    // move the ship animated to the touch position
    [ship2 runAction: [CCActionMoveTo actionWithDuration:1.f position:touchLocation]];
}

//method gets called every frame on every of your scenes
- (void)update:(CCTime)delta
{
    //move the ship only in the x direction by a fixed amount every frame
    ship1.position = ccp( ship1.position.x + 100*delta, ship1.position.y );

    if (ship1.position.x > self.contentSize.width+32)
    {
        //if the ship reaches the edge of the screen, loop around
        ship1.position = ccp( -32, ship1.position.y);
    }
}
```

Congratulations! If you got this far, you now know that your Cocos2D and Xcode installations work, you've learned the basics of navigating Xcode, and you've written some code in Objective C!