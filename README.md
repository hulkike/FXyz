FXyz3D
======

 - FXyz3D Core: 
 [ ![Download](https://api.bintray.com/packages/jpereda/FXyz3D/fxyz3d/images/download.svg) ](https://bintray.com/jpereda/FXyz3D/fxyz3d/_latestVersion)

 - FXyz3D Client: 
[ ![Download](https://api.bintray.com/packages/jpereda/FXyz3D/fxyz3d-client/images/download.svg) ](https://bintray.com/jpereda/FXyz3D/fxyz3d-client/_latestVersion)

A JavaFX 3D Visualization and Component Library

## How to build

The project is managed by gradle. To build, type

	gradle assemble

To deploy it to your local Maven repository, type:

	gradle publishToMavenLocal

## Use of FXyz3D Core

With FXyz3D there are many different 3D custom shapes. The following sample makes use of `SpringMesh` to create 
a 3D mesh of a spring.

![](/resources/SpringMesh.png)

### Sample

Create a gradle project, add the dependency:

```
repositories {
    jcenter()
}

dependencies {
    compile 'org.fxyz3d:fxyz3d:0.2.0'
}
```

and create a JavaFX Application class: 

```java
    @Override
    public void start(Stage primaryStage) throws Exception {
        PerspectiveCamera camera = new PerspectiveCamera(true);        
        camera.setNearClip(0.1);
        camera.setFarClip(10000.0);
        camera.setTranslateX(10);
        camera.setTranslateZ(-100);
        camera.setFieldOfView(20);
        
        CameraTransformer cameraTransform = new CameraTransformer();
        cameraTransform.getChildren().add(camera);
        cameraTransform.ry.setAngle(-30.0);
        cameraTransform.rx.setAngle(-15.0);
        
        SpringMesh spring = new SpringMesh(10, 2, 2, 8 * 2 * Math.PI, 200, 100, 0, 0);
        spring.setCullFace(CullFace.NONE);
        spring.setTextureModeVertices3D(1530, p -> p.f);
        
        Group group = new Group(cameraTransform, spring);
        
        Scene scene = new Scene(group, 600, 400, true, SceneAntialiasing.BALANCED);
        scene.setFill(Color.BISQUE);
        scene.setCamera(camera);
        
        primaryStage.setScene(scene);
        primaryStage.setTitle("FXyz3D Sample");
        primaryStage.show();
    }
```

### FXSampler

To use the FXSampler and visualize all the samples and the different options available, clone the repository, and run:

    cd Fxyz-Samples
    ./gradlew run
    
There is a hidden side popup menu at the left, from where different samples can be selected. From the right panels different options can be applied dynamically to the 3D shape.

![](/resources/fxsampler.png)


Special Thanks go to ControlsFX for providing the FXSampler framework.
http://fxexperience.com/controlsfx/
Our Sampler uses a heavily modified version, due to being 3D.
