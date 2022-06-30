# Image-Colorization

The task of colourizing black and white photographs necessitates a lot of human input and hardcoding. The goal is to create an end-to-end deep learning pipeline that can automate the task of image colorization by taking a black and white image as input and producing a colourized image as output.<br/>

<a href="url"><img src="https://user-images.githubusercontent.com/96406063/176648573-ffd59db0-431c-46b0-aa52-642a661229d5.png" width="720" height = "350">

## Methodology:

- The colorization of grayscale images can be thought of as an image-to-image translation task where we have the corresponding labels for the input grayscale image. A conditional GAN conditioned on grayscale images can be used to generate the corresponding colorized images.</br>
- The architecture of the model consists of a conditional generator with grayscale image inputs and a random noise vector and the output of the generator are two image channels a, b in the LAB image space to be concatenated with the L channel i.e. the grayscale input image.<br/>
- The generator is trained via adversarial loss, which encourages the generator to generate plausible images in the target domain. The generator is also updated via L1 loss measured between the generated image and the predicted output image. This additional loss encourages the generator model to create plausible translations of the source image.<br/>
- The discriminator is provided with both a source image and the target image and must determine whether the target is a possible transformation of the source image.<br/>
   
### RGB L*A*B

RGB operates on three channels: red, green and blue. Lab is a conversion of the same information to a lightness component L*, and two color components - a* and b*. Lightness is kept separate from color, so that you can adjust one without affecting the other. "Lightness" is designed to approximate human vision, which is very sensitive to green but less to blue. If you brighten in Lab space, the result will often look more correct to the eye, color-wise.<br/> 

<a href="url"><img src="https://user-images.githubusercontent.com/96406063/176662878-a3327a91-ea30-4600-ac23-9bb934b30de7.png" width="600" height = "350">


### Generator
The network used for generators in conditional GAN is not the same as conventional GAN. This is an encoder-decoder model which uses U-Net architecture. The model first downsamples the input image, to the bottleneck layer and then upsamples it from there to the final output image size. The arrows with a dotted line are called ‘skip connections’ which concatenates the output of the downsampling convolution layers with the feature maps from the upsampling convolution layers at the same dimension. As it is evident, the network is symmetric and hence, each downsampling layer will have a corresponding upsampling one which enables skip connections in between smoothly.<br/>
  
  <a href="url"><img src="https://user-images.githubusercontent.com/79749572/176718015-449f8120-1182-4efd-9381-0bc28bc0542a.png" width="600" height = "350">

### Discriminator
   Here we have used PatchGAN network for discriminator which classifies the patches of an input image as real or fake instead of the entire image. PatchGAN discriminator systemizes each NxN patch in an image as real or fake and then runs convolutionally across the image to return a single feature map of real or fake predictions that can be averaged to give a single score which is the final output D of the discriminator. An advantage of PatchGAN is that a fixed-size patch discriminator can also be applied to arbitrarily large images.<br/>
 
  <a href="url"><img src="https://user-images.githubusercontent.com/79749572/176719612-5686de87-e67d-4037-ac5f-d97c6a9a135d.png" width="600" height = "350">
  
  <a href="url"><img src="https://user-images.githubusercontent.com/96406063/176681673-337b10ab-ac3d-4552-9db5-f2d003ce0200.png" width="600" height = "45">
  <a href="url"><img src="https://user-images.githubusercontent.com/96406063/176681474-04b8e936-8095-4260-a4b4-e4d53f9047d7.png" width="600" height = "45">
<a href="url"><img src="https://user-images.githubusercontent.com/96406063/176681259-7b140bc9-9bc8-4d4c-bfce-5e5c47ede77a.png" width="600" height = "45">
      
### Results

  <a href="url"><img src="https://user-images.githubusercontent.com/96406063/176685572-d9e0a967-2709-49e6-80e0-de750f8b22a9.png" width="720" height = "350">
  <a href="url"><img src="https://user-images.githubusercontent.com/96406063/176715153-d17bf7f1-f7e3-439f-ad29-a0825bca1972.png" width="720" height = "350">
  <a href="url"><img src="https://user-images.githubusercontent.com/96406063/176715174-1c1bc074-dad8-4f75-a9da-461e131d4bf5.png" width="720" height = "350">
    
### References
  - Pix2Pix Image Translation Paper  (https://arxiv.org/pdf/1611.07004.pdf) <br/>
  - Pytorch Tutorials<br/>
  This project is done under the guidance of Vision And Language Group @IIT Roorkee
### Contributers
  <a href="https://github.com/praffulv-225">Prafful Varshney</a><br/>
   <a href="https://github.com/raosatyam">Satyam Yadav</a><br/>
