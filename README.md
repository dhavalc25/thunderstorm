## Abstract:

<p align = "justify"> We put forth a couple of simple processes of simulating a realistic looking Thunderstorm in 3D. We discuss various processes with which we can generate various aspects of a Thunderstorm, like clouds, lightning, rain, etc. with few advantages and disadvantages of each, and then describe in detail the approach we end up using for each of these aspect in our own simulation of a realistic Thunderstorm. We have also put links to the videos of our output for the readers to judge the visual performance of the approaches themselve. We have used Threejs, and Unity, to implement our cloud system, and lightning respectively, which can be used in real time applications like in games, movies, or creating some similar looking special visual effects. </p>

## Introduction:

<p align = "justify"> As keen consumers of movies, games and other forms of animation, we realized that clouds and lightning were two natural phenomenons that provoked lots of interest and fascination with respect to how they occurred and their visual characteristics. The lay observer may view them as arbitrary manifestations of the weather but to the keen ones, the processes of cloud formation and movement are incredibly interesting and infinitely dissectable. The same can be said for lightning which occurs in a much more specific setting, accompanied by thunder and quite often by rain or other forms of precipitation. Clouds are of several types, they may vary based on the weather in a particular location and also based on the height at which they occur. They can be spongy, dense and perhaps even a tad intimidating on an overcast afternoon while being relatively insipid and nebulous on a bright and sunny morning. Close observation readily reveals that clouds are not continuous objects but discrete particles that tend to cluster together in a myriad of shapes while displaying fascinating patterns of movement. Lightning bolts occur for frustratingly brief spans of time and show up as bright flashes of light that cascade mysteriously through the air, forming weird geometric patterns while doing so. Growing up, all of us were spellbound viewers of both phenomena and this effect has not left us even as adults. This is why we decided to attempt a project that would display realistic animation of both clouds and lightning on a stormy night. </p>

## What we set out to do:

<p align = "justify"> The main idea we decided to tackle was that of cloud formation and movement leading up to a thunderstorm, which would be followed by lightning bolts emerging intermittently from the clouds on a stormy evening. The animation would involve the clouds slowly forming and then darkening over time to the point where they warned of a coming storm. This involved bigger cloud formations in the sky followed by the start of the storm itself accompanied by the lightning. We intended our primary components to be the clouds and the lightning as we anticipated that creating these from basics would pose a satisfying challenge. We intended to explore various methods for illustrating these phenomena, like the dielectric breakdown model, and procedural generation for lightning, and particles, perlin noise, and volumetric rendering and textures for the clouds. We decided that other common components of thunderstorms such as rain, thunder and the motion of lights would all be supplementary to our core goals. If by the end we had not finished the core components, we could forego them. Otherwise, we could add rain using particles. Thunder could be included by syncing various sounds with the lightning. And finally, light interpolation could be achieved by illuminating the scene when the lightning strikes based on the location of the strike and its intensity. </p>

## Methodology:
### **Formation of Clouds: Techniques**
There are a handful of techniques that can be used to create photo-realistic clouds. We looked into a couple of them in-depth which are mentioned below.
#### **Particle System**
##### a) Unity Particle System
<p align = "justify"> Both our mid-quarter presentation demo and the final combined demo used the built-in Unity Particle System. The mid-quarter update used a single emitter while the final demo uses multiple emitters. The clouds are progressively darkened overtime and act as a harbinger for the coming thunderstorm. They are also programmed to move into the scene after a delay, stay in the scene during the thunderstorm accompanied by rain and lightning, and then proceed to drift away. We illuminate the terrain present in the scene whenever there is a bolt of lightning. We attempted to sync the thunder with the lightning but decided to play the sounds more at random because the number of lightning bolts we wanted to display during the sequence would have made it a little too noisy and cacophonous. Even if it might seem true to life to have the sounds, we decided to reduce the number them so as to spare viewers. We also attempted to illuminate the clouds during the lightning but could not get that done in time for submission unfortunately. </p>


##### b) Threejs Particle System
<p align = "justify"> Threejs has a more hands off approach when it comes to Particle System. All the particles need to be animated by iterating over them. Even though we could get semi-realistic clouds moving in the scene, we decided not to use it for any demos since it did not look as great as Unity's clouds and also the animation seemed a lot like our own particle system assignment just with a different kind of motion. </p>


#### **Volumetric Rendering and Textures**
<p align = "justify"> As we showed during the final demo, our original intention was to emulate the beautiful and realistic clouds Inigo Quilez had produced in [Video 01]. In order to do so, we used textures to create the structure of individual clouds in our scene and then added several of them close together to smoothen the edges between the clouds. The clouds are all generated along a plane in the scene and our camera just moves through them gradually while seemingly caressing them. When the number of clouds is less, our scene looks like this [Video 02]. In that scene, the texture being used to create the clouds are easily visible individually. Our 'remake' of Inigo's scene is here [Video 03]. For that we increased the number of clouds to increase the smoothness of their boundaries. We then increased the number of clouds and reduced the distances between them to show like this [Video 04]. In order to add to the 'cloudiness' of the scene, we also added particles to the scene which we call fog. This adds on to the fuzziness of the scene and we think it gives it an even more reslistic feel especially when flying through the clouds or just over them [Video 05][Video 06]. </p>

<p align = "justify"> The video [Video 07] demonstrates the approach and the composition of the scene. The clouds are just 2D mapped textures layered on top of and next to one another. With variable spacing for each layer but constant between them. They are all rendered on a plane which continuously renders more clouds as the user attempts to zoom into scene to get to the end of the plane. Some of the fine particles added to the scene are barely noticeable when panning around the scene. It is mainly the layering of the clouds and the camera's movement through them that produces the realism here. When one zooms in and pans to see the clouds from top or bottom, the 2D  clouds are clearly visible with small gaps between each layer. It's interesting that this scene could easily be used in a game to produce realistic looking clouds if the player is to just pass through them or just above them. From the player's point-of-view, the clouds are quite nice looking and wispy as expected. The exact same scene with another cloud texture is shown in [Video 08]. This shows how important a role the texture itself plays in the scene. This texture is whiter and wispier. The clouds no longer have clearly defined shapes and sizes. They all appear kind of fused together. Here is one more with another texture [Video 09]. This one is almost nebula like with an odd glow. All the clouds fuse to create a completely shapeless, homogeneous mass. </p>


#### **Perlin noise in Threejs**
<p align = "justify"> A method we were very intent on trying for producing clouds. Unfortunately, we didn't have enough time to do it properly. We were able to simulate basic noise but it does not resemble clouds closely enough to appear realistic. </p>


### **Formation of Lightning: Techniques**
We looked into the following three techniques to generate lightning patterns. 


#### **Unity3D Particle system lightning**
<p align = "justify"> The initial stage was developing a convincing effect using built-in tools offered by unity which would help in clearing any pre-conceived notions about the work at hand and also to have tested structure to work  upon. This was achieved using Unity3D's particle system by manipulating the emission and noise modules along with some other experimentations in number of particles and lifetime. This can be seen in this video. [Video 10]. </p>


#### **Fractal Dimension of Dielectric Breakdown**
<p align = "justify"> The initial approach was using fractals to simulate lightning based on a probabilistic approach to employ branching for the lightning with minimal randomness, the idea was to have an initial structure with pre-defined probabilities and once rendering goes into effect based on the  electric potential each point is assigned a value lower than 1 with all it's possible branches which totals to one and a single point is selected which is expanded all according to the electric potential defined values. The problem with this approach was that it did not allow room for manipulating the system for more unnatural animations and also it was computationally more expensive. This would have required the use of particle system of Unity3D. </p>


#### **Procedurally generated lightning in Unity**
<p align = "justify"> The implemented approach is to use a procedural algorithm that follows a recursive pattern that manipulates a single line renderer with pre-defined initial and end positions along with customizable number of split points in the line, the algorithm follows a recursive approach to break the line in parts and generate random position vectors for them to create a zig-zaggy line that simulates lightning and all it took was to adjust the start position along with a flickering renderer and an angle of rotation along one of the axis to develop a convincing effect. This can be seen in a scene developed in unity using particle systems for clouds and rain along with the procedurally generated lightning coupled with audio and visual synchronization in the following video. [Video 11] </p>


## Challenges:
##### 1. Working in a Team
<p align = "justify"> Working in a team is a good thing because it usually means that we have people around us that can help. While this is true, it is also important to note that communication is needed to successfully work in a team. In our case, although we had a good working relationship with each other, we had a hard time sitting and working on this project together because of very different individual schedules. We relied on offline communication for the most part of the development phase which created lags and ultimately delayed the integration phase. </p>


##### 2. Learning Unity
<p align = "justify"> Unity is a very powerful game-engine that can be used for creating complex virtual scenarios. However, there are specific ways of doing things in Unity and it requires for us to learn the tool as much possible as we can. This became a problem because none of us had ever used or worked with Unity ever before and most of felt comfortable in working with some other frameworks like Threejs. </p>


##### 3. Branched Lightning
<p align = "justify"> Real world lightning can have a million different shapes but there are some that can be generalized and classified into some categories. One of these categories is Branched Lightning. In Branched Lightning, there isn't just one continuous combination of lines, there are lines branching out of the main set of lines as well. Like a tree. We were unfortunately unable to implement this specific type of lightning successfully. The Line-Renderer object of Unity that we used to visually represent our lightning, created some problems while working with a recursive algorithm of lightning generation. We still haven't figured out the cause of this issue. </p>


##### 4. Global Illumination
<p align = "justify"> It was difficult to illuminate the part of particle system based Clouds from where a bolt of lightning appeared. Simply toggling a hidden light source didn't work because particles in Unity's particle system are not individual objects and they can't have a prefab of their own. </p>


## Future Work:
##### 1. Combine the threejs clouds with the unity scene 
<p align = "justify"> The Unity scene uses the particle system for the clouds. Since our team happened to have different skill sets with knowledge of varied tools, we set out to create our respective components using the tools we were familar with due to our assignments. We intended to combine the approaches at the end but due to wildly differing schedules and deadlines, we ended up compromising and demoing both separately. Combining the two would go a long way into producing an incredible looking scene. </p>


##### 2. Branched lightning 
<p align = "justify"> There were some problems we faced while implementing branches in the lightning in the recursive algorithm. Doing this would immediately make our scene's lightning a more spectacular entity. </p>


##### 3. Better looking clouds
<p align = "justify"> There is always room to tinker with the shaders to make the clouds look better. The distance function could also be tweaked. Even using a better texture could help with making the clouds look better. </p>


##### 4. Rain droplets
<p align = "justify"> Make the rain droplets look more realistic and possibly change directions periodically indicating the presence of strong winds during the thunderstorm. </p>

##### 5. Collisions
<p align = "justify"> This is mainly between the rain droplets and various objects in the scene and the terrain. Could be done once the rest of the scene is deemed satisfiable. </p>

##### 6. Puddles
<p align = "justify"> Rain during storm always produces large puddles that reflect the sky wonderfully. Also, rain droplets falling on the puddles and colliding improves the realism of the scene. </p>


## References:

<p align = "justify"> [1] Yun, Jeongsu and Son, Myungbae and Choi, Byungyoon and Kim, Theodore and Yoon, Sung-Eui. (2017). Physically inspired, interactive lightning generation: Physically-Inspired, Interactive Lightning Generation. Computer Animation and Virtual Worlds. e1760. 10.1002/cav.1760. </p>


<p align = "justify"> [2] Niemeyer, L and Pietronero, Luciano and J. Wiesmann, H. (1984). Fractal Dimension of Dielectric Breakdown. Physical Review Letters - PHYS REV LETT. 52. 1033-1036. 10.1103/PhysRevLett.52.1033. </p>


<p align = "justify"> [3] Hasan, M. Mahmud, M. Sazzad Karim, and Emdad Ahmed. "Generating and rendering procedural clouds in real time on programmable 3d graphics hardware." 9th International Multitopic Conference, IEEE INMIC 2005. IEEE, 2005. </p>
