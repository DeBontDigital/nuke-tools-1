# nuke-tools
A collection of some great tools for Nuke.

# Table of Contents

- [Gizmos](#gizmos)
  - [Overkill](#overkill)
  
# Gizmos

## Overkill
A tool to add muzzle flashes, bullet casing animations to a tracked gun.

*Usage Notes:*
- Currently only supports Python3.
- Currently only supports single fire.
- Currently only supports a single variant of muzzle flash and/or casing animation.
- Currently limited to 10 gun shots

![Overkill_github](https://user-images.githubusercontent.com/122035373/225667043-e3d97ce6-37db-438b-8f46-0a987ac7d912.png)


**How to use**

Make sure to prepare all the tracking data needed for the node.
In the demo file, we tracked the camera movement and used <a href="https://keentools.io/products/geotracker-for-nuke">Keentools GeoTracker</a> to track the gun animation. Afterwards we extracted the axis animation data out of the GeoTracker. 

The Overkill node contains 4 inputs:
- Gun_Mesh
- Gun_Axis
- Muzzle_Flash
- Bullet_Anim

Let's go over each input;

```Gun_Mesh```: **You don't have to provide this input**, but it can come in handy. Link it up with your 3D gun model, ideally the one used in your footage.

```Gun_Axis```: Make sure you hook this up with the 3D axis animation, which could be anything you created by hand or tracked. Just remember to use the axis node, otherwise, it won't work right.

```Muzzle_Flash```: Link this to your muzzle flash footage and make sure you adjust the timing so that the flash becomes visible from frame 0. This is the muzzle flash that you'll position at the front of your gun.

```Bullet_Anim```: Provide this input with the **3D** casing animation and ensure that the animation starts at frame 0. This will be the casing animation that comes out of the tracked gun.

To begin, position the muzzle flash appropriately, usually at the front of the gun, *aka the muzzle*. This can be done in the ```Muzzle Flash``` tab. Make sure your 3D gun and muzzle flash footage is loaded in on beforehand. Set the footage length of the muzzle flash in the *"Footage Length in frames"* knob. Next, check on the *"Muzzle Configure Mode"*. In your 3D viewport, you should see a card with your muzzle flash, a sphere, and your 3D gun model. Place the sphere at the muzzle, which is where the muzzle flash is emitted from. Afterwards you can offset the card so it aligns accordingly. If the help-sphere is blocking the view, you can uncheck *"3D Position Sphere"*. Once you have aligned everything, you can disable *"Muzzle Configure Mode"*.

Now, it's time to adjust the timing of the gunshots. Note down the number of times the gun is fired and the corresponding frame number for each shot. In the ```User``` tab, specify the number of shots in the *"number of gunshots*" field. Next, navigate to the ```Single Shots``` tab and enter the frame numbers for each gunshot.

Once you have everything correctly positioned and linked up, connect this node to a ScanlineRender with the tracked camera and composite the resulting output over its corresponding footage! The muzzle flash is also incorporated into a new channel named "muzzle_flash".
