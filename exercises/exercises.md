# Part 1
## Using Bioformats
Let's import a microscope specific file format into
Fiji.

1.  Open the image sted-confocal.lif with
    `[Plugins > Bio-Formats > Bio-Formats Importer]`.

2.  In the next dialog, you can select various import options. Make sure that you load
    the data into a Hyperstack and tick the Display metadata option.

    ![Bioformats import dialog](fig/bioformats-import-dialog.png){#fig:adj-bri width="63%"}

3.  The next window allows you to select a series. Several microscope
    image formats are actually libraries of files. In this case, you
    should see three different files. Open one of the series.

4.  Two windows are opened. One showing the image, the other showing the
    metadata information. Scroll through the information and find the
    Dimension Length, Number of Elements and Unit. Use these values to
    calculate the pixel size.
### tags: exercise bioformats-1

## Using OMERO
Now let’s try to utilize OMERO and load the image file sted-confocal.lif into the Omero database:
1. Start the Omero.insight software. Open the config window by clicking the little wrench and enter the server address omero-1.cecad.uni-koeln.de. Enter your credentials an connect to Omero.

2. Unfold the Display Groups dropdown menu in the toolbar and tick the All Members checkbox in the course group.

3. Start the importer (toolbar icon with blue arrow and colorful circles). Select the file sted-confocal.lif from your local harddrive for upload. Create your own project and dataset, start the import and close the importer when done.

4. Update the projects view (icon on top of the Project pane) and find your uploaded file. Explore the metadata (acquisition pane, on the right, check if you can download your original data again and leave a comment and a rating to at least one of the images.

5. Close the insight client, start the webclient (i.e.  open https://omero.cecad.uni-koeln.de in your favorite webbrowser), find your image and compare the handling of insight and webclient.

6. Now try to load the image from Omero in Fiji. If the required plugin is already installed, you will find the entry OMERO in the Plugins Menu.Select Connect to OMERO. Login again and choose your image in the Omero window.
### tags: exercise omero-1

## Scale Bars
Let's explore one thing you usually have to include in your
microscopy data: a scale bar that indicates the size of each pixel.

1.  Open the image sted-confocal.lif in FIJI from OMERO
    `[Plugins > OMERO > Connect to OMERO]`.

2.  We now want to add a scale bar to our image. In this case, Fiji
    already knows the pixel size - let us check whether our previous
    calculations were correct. Go to `[Analyze > Set Scale...]`. This
    dialog should show you how many pixels are in one micrometer.


3.  In case you have an image where information about the scale is
    visible in the image itself, you can then measure the length with a
    line and include this information in the dialog. Clicking on Global
    helps if you take one image of a micro-scale and want to use this
    information in other images you took with the same settings (e.g. on
    a small Lab-Microscope).

4.  Let's add a scale bar now. Use `[Analyze \> Tools \> Scale Bar]`.
    Similar to the calibration bar, the dialog lets you adjust various
    visual parameters .

5.  Now open the file using Omero.insight again. Double click the image
    to open a viewer window. Use the Display menu to add and adjust a scalebar. Export the image (toolbar icon with image and red arrow). 
### tags: exercise scalebar-1

## Brightness Adjustments

1.  Open the file fibroblast_sim.tif from OMERO in Fiji. This is a 16-bit
    gray-scale image showing actin filaments in a cell.

2.  You should note that the image looks rather dark. Fortunately, Fiji
    has a way to adjust the brightness and contrast of an image without
    altering the original data. Go to
    `[Image > Adjust > Brightness/Contrast...]`, you should see a dialog as shown in the figure.
 ![Adjust brightness dialog](fig/adjust-brightness-dialog.png){#fig:adj-bri width="23%"}
    
3.  Click on `[Auto]`. The image gets brighter as the maximum brightness
    is now associated with a lower image intensity. This linear scale
    can be adjusted manually by changing the slider positions. `[Reset]`
    reverts to the original intensity scaling.

4.  Play with the sliders to set the image intensity scaling.

5.  Using `[Set]`, we can either enter precise minimum and maximum
    values or show a defined range (8-,10-,12-,15-,16-bit) and also
    propagate our selection to all other open images. Again, the
    original pixel values remain, we only change the display.
### tags: exercise brightness-1
\pagebreak
\newpage
## Contrast Enhancement and Image Manipulation 
Let's assume you want to
show gel data in your manuscript. After performing following steps, can
you discuss why contrast enhancement might be considered fraud?

1.  Open the image gel.tif and duplicate the image (another
    Fiji sample image).

2.  Adjust Contrast and Brightness and compare images. What is the
    problem with the contrast-enhanced image?
![Contrast problem](fig/contrast-problem.png){#fig:contrast-problem width="65%"}   
### tags: exercise brightness-2
\pagebreak
\newpage

## Bit-Depth Conversion

1.  Open the image beads.tif from OMERO.
    Duplicate the image with `[Image > Duplicate...]`. Choose the line
    selection tool and draw a line through one of the bright spheres in
    the image. 
![Line ROI example](fig/line-roi-example.png){#fig:line  width="75%"}
    
2.  In the next step, we will look at the intensity (brightness)
    distribution along this line. For this, do
    `[Analyze > Plot Profile]`. You should observe that the
    gray value (y-axis) ranges from 0 to 65535 and that the curve looks
    cut at the upper end - this means that we have *saturated* pixels,
    i.e. we cannot resolve any differences between these saturated
    pixels although the shape of the curve would suggest intensity
    changes. The \[Plot Profile\] function allows you to list (show),
    save and copy the values. If you click on `[Live]`, you can change
    the line ROI and the plotted profile will update. Try the update by
    drawing a line somewhere on the background and then again through a
    bead. Turn the live mode off again by another click on the button.

![Plot profile example](fig/plot-profile-example.png){#fig:ppe width="55%"}    

3.  Now, we convert the 16bit image to 8bit. First, we make sure that we
    scale during conversion by `[Edit > Option > Conversion]`. Then, we
    use `[Image > Type > 8-bit]` to convert the image. Make sure that
    the line ROI is still there and perform the plot profile function
    again. A second window pops up. Compare the plot profiles of the
    8-bit and the 16-bit images. The conversion modified the brightness
    value (y-value). While the profiles are similar, the scaling is
    different. The image is scaled according to following equation:
    $$I_{8bit}=\frac{I_{16bit}(x,y)-min(I_{16bit}(x,y))}{max(I_{16bit}(x,y))-min(I_{16bit}(x,y))}*2^8$$
    with:\
    I~16bit~(x,y): 16bit image\
    I~8bit~(x,y): 8bit image\
    max(I~16bit~(x,y)): maximum value of 16bit image\
    min(I~16bit~(x,y)): minimum value of 16bit image\

4.  Convert the image back to 16-bit and check the intensity values
    again. In this case, the intensity values are not increased.

5.  The conversion actually looks at the data as it is displayed. Adjust
    the brightness and contrast to an extreme value using
    `[Image > Adjust > Brightness/Contrast...]` (contrast slider to the
    right edge). Convert the image to 8-bit again. Look at the profile
    of a bead. You should see that the image only consists of 2
    intensities: 0 and 255. As you saw, it is important to reset the
    brightness and contrast display before converting the image.
### tags: exercise bitdepth-1
\pagebreak
\newpage

## Viewing a 3D Stack

1.  Open the file flybrain-template.tif from OMERO. This is an 8-bit
    gray-scale z-stack, showing a standard template of a fly brain. You
    should see that there is a slider below the image to go through
    individual z-sections of the stack.

2.  If the image looks too bright or dark, adjust the brightness
    (`[Image > Adjust > Brightness/Contrast...]`).

3.  Click on the start animation button left to the slider to start an
    automatic stepping through the sections similar to a video).
    Clicking on the button again, pauses the animation (button icon
    changes accordingly).
![Stack animation](fig/stack-animation-button.png){#fig:stanbu width="25%"}   
    
4.  Using the stack toolbar, you can `[Start Animation]` and
    `[Stop Animation]` as well.
![Stack animation](fig/stack-toolbar.png){#fig:statob width="85%"}   


5.  Use the `[Animation Options]` from the stack toolbar to increase the
    animation speed to 20 fps (frames-per-second) and loop back and
    forth. The animation should look much smoother now.
![Stack animation](fig/animation-options-dialog.png){#fig:anopdi width="25%"}   

6.  When you want to use an animation of the stack in a presentation,
    you can save the stack as an avi using `[File > Save As > AVI...]`.
### tags: exercise animation-1
\pagebreak
\newpage


## Order of Dimensions

1.  Open the file flybrain-template.tif if it is not still
    open.

2.  Use `[Image > Hyperstacks > Stack to Hyperstack...]` to convert the
    stack to a hyperstack. In our test image, the order, channels,
    slices and frames should be detected correctly.

3.  Now, you can easily re-order the dimensions of the hyperstack using
    `[Image > Hyperstacks > Re-order Hyperstacks...]`. Although this
    does not make any sense, change the z-dimension to a time dimension.
    As you can see, from the user perspective, this does not change
    anything at the moment.
### tags: exercise dimensions-1
\pagebreak
\newpage

## Manipulating Stacks -- Creating a Montage 

A common way 3-dimensional
data is presented (typically along time or z-axis) is the montage view.

1.  Open the file flybrain-template.tif if it is not still
    open.

2.  Use `[Image > Stacks > Make Montage...]`. In the dialog, set
    `[Columns]` and `[Rows]` to 5, `[First Slice]` to 100,
    `[Last Slice]` to 124, change the `[Border Width]` to 1 pixel and
    tick `[Label Slices]`.

    ![Make montage dialog](fig/make-montage-dialog.png){#fig:mmdia width="21%"}   



3.  You can see how easy it is to create a custom montage view, play
    with the different options, e.g. `[Increment]`.
### tags: exercise montage-1
\pagebreak
\newpage

## Manipulating Stacks -- Creating an Insert
We now want to do something
more complicated: let's say we want to show a detail of the flybrain,
e.g. the central complex or the optic lobes. To help viewers, we want to
put a little version of the complete brain in the corner of our 3D image
as an overview. How would you proceed?

1.  Open the file flybrain-template.tif if it is not still
    open.

2.  Use the rectangle tool to select an interesting part of the brain
    that you want to highlight. Duplicate the complete stack using
    `[Image > Duplicate]`, this will only duplicate the part you
    selected.

3.  Use `[Image > Adjust > Size...]` to create an image with 1024 pixel
    width and no interpolation.

4.  Go back to our original image of the fly brain and use
    `[Image > Scale...]` to reduce the image size to 20% (x, y) with
    bilinear interpolation.

5.  The insert is created with `[Image > Stacks > Tools > Insert...]`.
    Make sure you use the detailed view of brain as `[Destination]` and
    the overview as `[Source]`. `[X-Location]` and `[Y-Location]` can
    remain 0.

![Stack inserter](fig/stack-inserter-dialog.png){#fig:stains width="25%"}  

6.  Again, a very easy procedure -- explore further stack operations on
    your own.

### tags: exercise insert-1
\pagebreak
\newpage

## RGB Images

1.  Download the file muscle-cell.tif from OMERO and open it with FIJI. (Alternatively open the image via the Fiji-Plugin, however, this converts RGB images by default into 3 channel composite images. So you have to convert the image in Fiji to RGB then by  `[Image > Type > RGB Color]`.  This image was taken
    from a publication in Nature Cell Biology 5, 598(2003); Cell of the
    Month: The vascular smooth muscle cell cytoskeleton; Mario Gimona;
    DOI:10.1038.ncb0703-598. This RGB image shows mouse smooth muscle
    cell with fluorescent labels of the cytoskeleton. Use
    `[Image > Show Info...]` for details about this image.

2.  Use `[Image > Adjust > Brightness/Contrast]` and change the slider
    values. Observe that this operation affects all colors
    simultaneously. Reset the changes.

3.  We now split the red, green and blue channels of the RGB image with
    `[Image > Color > Split Channels]`. Three windows appear, each
    showing the respective color content.

4.  Let's combine these channels again with
    `[Image > Color > Merge Channels]`. The merge-function gives us many
    options to create a merged image. Do not set any options and
    use the same color channels.

![Merge channels](fig/merge-channels-dialog.png){#fig:mrgchn width="23%"}   

5.  Now split again and merge back, but with option `[Create composite]`
    ticked. This creates a slider below the image, indicating that we
    created a three-layered stack, one layer for each color.

6.  The composite image allows us to work on each channel separately.
    Perform `[Image > Color > Channels Tool...]`. In this dialog, you
    can select individual channels in composite mode or view individual
    channels in Color/Grayscale mode. Try out the different
    settings.

![Stack animation](fig/channels-tool-dialog.png){#fig:chntls width="22%"}   
    
    
7.  Try to perform already known operations on just one color channel,
    e.g. adjust the brightness (you can see that the little histogram
    changes color when you change the channel!).
### tags: exercise rgb-1
\pagebreak
\newpage

## Exploring Lookup Tables

1.  Open the image beads.tif. You can look at the LUT of
    the current image with `[Image > Color > Show LUT]` which is the
    standard linear grayscale LUT you have already seen.

2.  Change the LUT using `[Image > Color > Edit LUT...]`. Click on the
    top-left dark value and change the color from black to blue, select
    the white entry from the bottom right and change the color to red.

![LUT Editor](fig/lut-editor.png){#fig:lut-editor width="40%"}
    

3.  Look at the image. Does it look familiar? This is the HiLo LUT that
    is often used in microscopy to optimize parameters for acquisition
    (emitted light, gain, offset). You can obtain the same image by
    selecting the HiLo LUT in Fiji.

    ![LUT Tools](fig/lut-tool.png){#fig:lut-tool width="80%"}


4.  Close the image and open the file cell-colony.tif.
    Change the LUT to Spectrum using
    `[Image > Lookup Tables > Spectrum]`.

5.  Display the current LUT of the image. Try out different available
    LUTs and display their profile.


![Lookup Tables in
Fiji](fig/lookup-tables.png){#fig:lookup-tables width="80%"}
### tags: exercise lut-1
\pagebreak
\newpage

## Effects of LUT Changes

1.  Download the file muscle-cell.tif from OMERO and open it with FIJI. (Alternatively open the image via the Fiji-Plugin, however, this converts RGB images by default into 3 channel composite images. So you have to convert the image in Fiji to RGB then by  `[Image > Type > RGB Color]`.

2.  Simulate color-blindness with
    `[Image > Color > Simulate Color Blindness]`. This function only
    works on an RGB image.

3.  Use `[Image > Color > Replace Red with Magenta]` to exchange colors
    and then simulate color-blindness again. Color differences are much
    more obvious in the second image.

4.  Go back to the original image of the muscle and split the channels.

5.  Duplicate the window containing the blue channel information.

6.  Change the LUT to spectrum and discuss the differences between the
    gray and spectrum LUTs.
### tags: exercise lut-2
\pagebreak\pagebreak
\newpage

## Calibration Bars 
A calibration bar is typically added to a figure when
intensity comparisons are made. A calibration bar indicates which color
corresponds to which brightness. This is especially important when you
use LUTs with more than one color or when you use a single color LUT
where the change in intensity is not linear ('gamma').

1.  Open the image fibroblast-sim.tif.

2.  Adjust Brightness/Contrast and select a LUT you like.

3.  Add a calibration bar with \[Analyze \> Tools \> Calibration
    Bar\...\]. In the dialog, choose a location, fill color, label
    color, number of labels, asf. Note that this calibration
    bar shows the brightness settings you just applied and that you
    cannot change those now.

![Calibration bar](fig/calibration-bar-dialog.png){#fig:calbar width="25%"}   


### tags: exercise calibrationbar-1
\pagebreak
\newpage

## Working with 5D Data 
To illustrate working with 5D data, we will import
a sequence of files that are labeled with \_t000_z000_c000 and
increasing numbering. The sequence of files has been generated from the
standard Fiji sample Mitosis
`[File > Open Samples > Mitosis (26 MB, 5D stack)]`. This data shows
Drosophila S2 cell expressing GFP-Aurora B and mCherry-tubulin fusion
protein undergoing mitosis (Courtesy of Eric Griffis).

1.  Open OMERO.insight and download all the files from the mitosis dataset (user: Peter Zentis). Do you see any problem about downloading these files using the OMERO.web client? In the OMERO.web client also try to apply an export script to the complete dataset, i.e. first select the mitosis dataset, then click on the cogwheel icon in the top menu bar and navigate to export_scripts>Batch Image Export...

2.  Go to `[Plugins > Bio-Formats > Bio-Formats Importer]` and select
    the first image in the folder of the downloaded images.

2.  The Bio-Formats import options dialog shows up, make sure to select
   `[Group files with similar names]`.

3.  In the dialog, you can choose how to stitch the files. We select "Pattern". This
    parses the file based on:
    mitosis_t0\<01-51\>\_z00\<1-5\>\_c00\<1-2\>.tif. \<\> denotes the
    range of the import, e.g. we could only select one channel, or any
    other substack.

![File stitching](fig/bioformats-file-stitching.png){#fig:bfs width="85%"}   

4.  The imported image shows three sliders: channel (2), z-position(5),
    time-stamps(51). Browse through the image, adjust Brightness if
    necessary. Upload the created flybrain image stack to OMERO. Open the original image`[File > Open Samples > Mitosis (26 MB, 5D stack)]` and compare with our version. One thing to notice is that we lost information about the
    z-spacing, distance between time-stamps or channel colors.
### tags: exercise 5d-data
\pagebreak
\newpage


## Projection (Dimensionality reduction) 
In a projection, data is summarized along one
axis (dimension). A typical case is the maximum intensity projection of
the z-axis of a 3D stack, resulting in a 2D image where each pixel
represents the maximum value that was found in this *(x,y)* position
along *z* - which is then used for the manuscript. In Fiji, you can
choose between the minimum, average or maximum intensity projection and
the sum, standard deviation or median of each pixel along *z*. Remember
that you can swap dimensions with
`[Image > Hyperstack > Re-order Hyperstack]`.

1.  Open the image GMR-10A12-AE-01.tif. This image shows
    the expression patterns of a GAL4 line, displayed on a standardized
    fly brain template (credits belong to the Rubin-lab, JFRC (Arnim
    Jennet) and The Virtual Fly Brain). Try to estimate the expression
    pattern (green) by going through *z* using the slider.

2.  In this case, we might decide a z-projection is helpful to quickly
    determine whether the expression pattern is of interest. We can
    perform the projection with `[Image > Stacks > Z Project...]`,
    choosing Max Intensity.

    ![Z-projection dialog](fig/z-projection-dialog.png){#fig:zprojd width="25%"}   

3.  Explore various projections on the flybrain stack created previously.
### tags: exercise z-projection-1
\pagebreak
\newpage

## Orthogonal View 
Another very common visualization is the orthogonal
view. In this view, two additional windows are created that are linked
to the current slider position of the 2D view. These windows show the XZ
and YZ position. This visualization can be useful if you want to present
the intensity profiles in 3D data while presenting overview images for
the orientation of the reader at the same time.

1.  Open the stack GMR-10A12-AE-01.tif. Show the orthogonal view with
    `[Image > Stacks > Orthogonal Views]`. Try scrolling through the
    axes to get a feeling for this view.
### tags: exercise ortho-view-1

## Color Coding
One option to add a third dimension on a 2-dimensional plot
is to somehow code the information; e.g. using different colors for
z-depth or time. This can be useful when the data is structured along
one axis, e.g. different layers of cells within a tissue, axons growing
into other tissue parts or vesicles moving around over time.

1.  Open the image fake-tracks.tif (another Fiji sample
    image). We use a fake file to better illustrate how the color coding
    works, but you can apply it to any 3D data for further testing.
    Perform `[Image \> Hyperstacks \> Temporal-Color Code\]` and select a
    LUT of your choice. Due to a bug in FIJI you might get an error message. To fix replace the file Temporal-Color_Code.ijm in plugins/Scripts/Image/Hyperstacks/ with the version provided in the sciebo folder.

![Color code](fig/color-code-dialog.png){#fig:cocodi width="25%"}   



2.  Compare the color-coded image with the original time-series.
### tags: exercise color-coding-1
\pagebreak
\newpage

## Generating a Kymograph Plot 
A Kymograph is an visualization to present a
dynamic process in a single image where movements along a line are
plotted for all time-frames in a stack (*x-t* plot). Therefore, it is
also a way to reduce dimensionality. They are common to show cellular
components moving along some path (e.g. mitochondria moving along an
axon or cells migrating in reference to a body axis during development).

1.  Open the stack axon-mitos.tif (Image by Arun
    Akondadi, Rugarli Lab, University of Cologne). Adjust Brightness.
    This image shows mitochondria moving along an axon.

2.  This image has a problem: the axon was not stained itself, but we
    can hopefully reconstruct the axon path by the positions of the
    moving mitochondria. For this, perform a maximum projection over
    time.

3.  The maximum-intensity image helps a lot to estimate the axon
    position in the image. Right-click on the \[Line-Tool\] to change
    the Straight Line to a Segmented Line. Use the segmented line
    to trace the axon path. A double-click ends the line.

![Segmented line tool](fig/segmented-line-selection.png){#fig:seglins width="85%"}   


4.  Go to the original stack and do
    `[Edit > Selection > Restore Selection]`. This restores the line we
    just selected on the maximum projection on the stack.

5.  Use `[Image > Stack > Reslice]` to generates the Kymograph. For
    display reasons, you can also invert the image with
    `[Edit > Invert]` and Adjust the Brightness.

6.  If the line was placed correctly, you should see something similar
    to the figure below. The kymograph helps to distinguish
    stationary mitochondria and we can sometimes even distinguish
    anterograde from retrograde movement (in reference to soma).

![Kymograph](fig/kymograph.png){#fig:kymo width="85%"}   
### tags: exercise kymograph-1

\pagebreak
\newpage

## 3D View 
Instead of trying to visualize our data in 2 dimensions, we can
also visualize in 3D using the 3D viewer in Fiji. For visualizations in
3D, several display options are common: Volume, Orthoslice, and Surface.
While this choice is obviously not available for printed figures, online
publishing of supplementary videos can be a good option to present your
data.

1.  Open the stack GMR-10A12-AE-01.tif from OMERO if it is not
    already open. Select the 3D viewer with \[Plugins \> 3D Viewer\]. In
    the options dialog, select the image and display as
    a volume.

![3d viewer dialog](fig/3D-viewer-dialog.png){#fig:threedv width="25%"}   


2.  Depending on your hardware, this might take a while to display. Try
    to navigate the 3D view with your mouse.

3.  Let us try to generate a movie that you can save as an avi file. Use
    the 3D viewer menu to create a simple 360 degree rotation with
    `[View > Record 360 degree rotation]`. This generate a stack that
    you can now save as a movie using `[File > Save As > AVI]`. In this
    dialog, you can set the compression as well as the frame rate (how
    fast the movie is displayed). For our purposes, we set the
    compression to uncompressed and the Frame Rate to 15 fps
    (frames-per-second). Movie generation for journals can also be a
    tricky thing as they often impose strict size limits and require
    specific formats. You often need to adjust the movie size as well as
    the compression algorithm to adhere to these requirements and the
    choice of both can be complicated. However, you can usually accept
    some compression artefacts as movies are often not considered raw
    data but more of a nice additional visualization. Still, make sure
    that you adhere to scientific principles and tell specifically how
    you treated your data to generate the movie.

4.  Further instructions on the 3D viewer can be found at:
    https://imagej.net/3D_Viewer.
### tags: exercise 3d-viewer
\pagebreak
\newpage

## Resampling Example - No Interpolation

1.  Open the file resampling-test.tiff from OMERO. This is a 20x20
    pixel black-and-white (binary) image. Use the magnification tool to
    zoom to the maximum magnification. You should now see a one pixel
    wide and a two pixel wide vertical white line and a 1px diagonal
    line.

2.  Before we perform image manipulations, we duplicate the original
    image for convenience `[Image > Duplicate]`.

3.  Go to \[Image \> Adjust \> Size\].

4.  Perform a resize to 30 x 30 pixels (150% size), with no
    interpolation, and compare the result with the original figure. Use
    the `Line-Tool` to measure the width of both vertical
    lines. You should observe that one line was not scaled while the
    other was scaled to 150%.

5.  Try other values for the resizing and observe the results.
### tags: exercise resampling-1

## Resampling Example - With Interpolation

1.  Again, work on a duplicate of the resampling-test.tif image.

2.  Adjust the size to 150% with interpolation set to 'Bilinear'. Use
    the `Point-Tool` and move the mouse over the image. On the bottom of
    the Fiji bar, you should see the mouse position in pixels and the
    value of the current pixel.

3.  While the interpolation helps to visually estimate the 150%
    re-sampling in the vertical and diagonal lines, you can see that the
    original data has been changed.

4.  Try other values for the resizing and observe the results.
### tags: exercise resampling-2

## Omero.figure - Image with scalebar

1.  Login into Omero.web. Find the image sted-confocal.lif \[Fab
    Antikoerper\] in the projects pane and right-click on the entry in
    the Project Explorer file list.

2.  In the context menu, select \[Open with \> Omero.figure\]

3.  A new figure window with the selected image opens up. First of all,
    press the **Save** button.

4.  To make sure our image is the active element in the figure, click on
    the image. Then have a look at the Info tab of the tool panel.
    Adjust the width and height until the image has a resolution of
    about 300 dpi.

5.  Now select the Preview tab. Change the color of the LUT and adjust
    the brightness as you like.

6.  Now, select the Labels tab. Add a scalebar (**Show** button)
    activate the scalebar label and adjust position, size and color of
    the scalebar as you like.

7.  Add some text to the figure legend. Try the suggested Markdown
    syntax if you like.

8.  **Save** the figure again. **Export** to pdf, Tiff (300dpi), and new
    Omero Image.

9.  Note that the exported figures were added as attachement to the
    original image.
### tags: exercise omero-figure-1

## Omero.figure - Creating multipanel figures

1.  Add another page to the figure \[File \> Paper Setup\... \> Number
    of Pages\]

2.  Select the new page. Now we would like to add the image
    sted-confocal.lif \[Overlay001\]. So change back to the project
    explorer and select the image (Left-click). In the top left corner
    of the General tab, click the Link button (chain symbol) and copy
    the link from the popup. Switch back to the Figure-tab and click the
    **Add Image** button in the menu bar. Paste the link into the
    textbox and click **Add Image**.

3.  Move the image to the second page of the figure. In the Info tab
    click on the chain symbol to lock the aspect ratio of the image,
    then change the width to 150. Click the **Set dpi** button and enter
    a value of 600 dpi.

4.  Switch to the Preview tab. Change LUT of the second channel to red
    and adjust the brightness of the individual channels.

5.  Switch to the Labels tab. Press the **Edit** button. Draw a small
    square shaped ROI (press shift while drawing) in an interesting
    region of the image. Set the line thickness to 10, choose a color.

6.  Press the **Show** button in the Scalebar section. Adjust size and
    color switch on the label.

7.  Write 'Merged' in the textbox in the Add Labels section. Change the
    font size to 18 and make sure position is set to Top. Click **Add**.
    Now replace 'Merged' in the textbox by 'Overview', switch Position
    to Left Vertical and click **Add** again.

8.  Copy and paste the image five times. Arrange them into two row of
    three images. After roughly moving the images in place, select them
    all and use the**Align to Grid** button in the menu bar for quick
    alignment.

9.  Select the second image in the first row. Switch to the Preview tab
    and switch off the second channel. Now switch to the Labels tab.
    Delete the Overview label. Change the 'Merged' label to 'Confocal'.

10. Select the third image in the first row. Switch to the Preview tab
    and switch off the first channel. Now switch to the Labels tab.
    Delete the Overview label. Change the 'Merged' label to 'STED'.

11. Select the first image in the second row. In the Labels tab delete
    the Merged label and change the 'Overview' label to 'Magnified ROI'.

12. Switch to the Preview tab. Press the **Crop** button. Select the ROI
    from figure and click **OK**. Confirm the deletion of the ROI in the
    cropped image. In the Labels tab adjust the scalebar size if
    necessary.

13. In the further images switch off one channel as in the first row,
    delete all labels, crop and adjust scalebars in the same way.

14. Save the figure.
### tags: exercise omero-figure-2

## Omero.figure - Limitations
1. Please try to create a figure in OMERO.figure similar to the figure created in the exercise "Manipulating Stacks - Creating a montage" in FIJI.

2. Review the exercises on creating inserts, calibration bars, z-projections and so on and think whether it would be (easily) possible to implement them in OMERO.figure as well.
### tags: exercise omero-figure-3
\pagebreak
\newpage
# Part 2


## Working with histograms

1.  Open the image hela-cells.tif. This is another
    standard Fiji sample image showing HeLa cells. Lysosomes are red,
    mitochondria green and the nucleus blue.

2.  We can show the histogram with `[Analyze > Histogram]`. The
    histogram is displayed in a new window. The x-axis shows the pixel value and
    the y-axis the count. Note that the histogram refers to the channel
    that was active when the command was called.


![Histogram](fig/histogram.png){#fig:histog width="25%"}   


3.  Obtain the highest and lowest intensities from the histogram. What
    does the histogram range tell you?

4.  Click on \[list\] to obtain a list with values and counts. \[Log\]
    displays the same histogram on a log-scale.

5.  Click on \[live\] in the histogram dialog and change the channel.
    Observe the changes in the histogram and note the color changes in
    the depicted colormap bar.
### tags: exercise histogram-1 
\pagebreak
\newpage

## Working with ROIs 1

One of the operations you can perform on a ROI is cropping:

1.  Open any image. Duplicate the image. Select a region by a
    rectangular ROI. Then, perform `[Image > Crop]` on the duplicate.
    Close the cropped image.

2.  Duplicate the original image again. Use the freehand selection to
    create a ROI on the duplicate. Crop the image. Note that the minimum
    and maximum values of your ROI have been used to determine a
    rectangular selection for the cropping.
### tags: exercise roi-1

## Working with ROIs 2
ROIs can be used to create image masks. An image mask is a binary image
that defines which parts of the image are of interest.

1.  Open any image. Duplicate the image. Create a few circular ROIs
    (press \<shift\> during creation to keep multiple ROIs).

2.  Use `[Edit > Clear Outside]` and then `[Edit > Fill]` to generate a
    mask image (this should look similar to fig.
    [\[fig:binary-mask\]](#fig:binary-mask){reference-type="ref"
    reference="fig:binary-mask"}. The 'Clear' command fills the
    respective area with the background color, 'fill' with the
    foreground color.


![Binary Mask](fig/binary-mask.png){#fig:binary-mask width="65%"}   
   

3.  Undo what you have done with `[Edit > Undo]`. You will notice that,
    in contrast to other programs, Fiji only allows to undo the most
    recent operation. This is done to minimize memory consumption.
    `[File > Revert]` allows you to go back to the last saved state.

4.  Go back to the original image. Use the command
    `[Edit > Selection > Create Mask]` to directly generate a mask
    image.
### tags: exercise roi-2

## Working with ROIs 3
Operations are usually performed on the selected ROIs and on the whole
image if no selections exist.

1.  Open any image. Duplicate the image. Select any ROI you like.

2.  Observe that `[Edit > Invert]` only affects the selected pixels.
    Undo the inversion.
### tags: exercise roi-3

## Working with ROIs 4
Finally, there are several operations that work on a ROI itself without
changing pixel values `[Edit > Selection > ...]`. Let us explore a few of those
options.

![Selection options](fig/selection-options.png){#fig:selection-options width="65%"}   
   
1.  Open an image, duplicate and draw a freehand selection with an
    outline that includes inner parts that are not selected. Fit a
    spline `[Fit Spline]`. This creates a smoothed version of the
    selection where individual points can now be dragged around and the
    shape can be changed. This can be useful to correct the outline of a
    shape (e.g. a worm or a cell).

2.  Use `[To Bounding Box]`. This creates a rectangular region that just
    fits over the selection (this is the same as the crop area). Undo
    the last operation.

3.  Use `[Convex Hull]`. This creates an outline of the selection, where
    a straight line between every pair of points within the ROI is also
    within the ROI (Definition of a convex object in Euclidean space).
    This can be useful if you want to measure the extent of an object
    with an irregular shape. Undo the last operation.

4.  Explore the operations `[Scale]`, `[Make Inverse]`, `[Enlarge]` and
    `[Rotate]`.

5.  Each ROI has properties that can be displayed and changed with
    `[Properties]`. Especially useful when you work with multiple ROIs
    (and the ROI Manager, see below), can be ROI names. If you need the ROI coordinates
    outside Fiji, you can list the coordinates of the ROI as well.

![ROI properties](fig/roi-properties.png){#fig:roi-properties width="25%"}   
### tags: exercise roi-4
\pagebreak
\newpage

## Working with the ROI Manager

1.  Open the image hela-cells.tif.

2.  Open the ROI Manager with `[Analyze > Tools > ROI Manager...]`.

3.  For the following analysis, we will only work on the bottom-most
    cell. Select the blue channel showing the nucleus. Use the ROI tools
    to create an accurate outline of the nucleus and add the selected
    region to the ROI manager. Rename the ROI to 'Nucleus'.

4.  Select the blue channel showing the mitochondria. In this channel,
    we can estimate the cell outline - create the outline and add the
    selected region to the ROI manager, rename ROI to 'Cell'.

5.  Let's say the task we want to solve is get the area of the cell,
    excluding the nucleus, for our further analysis. We now explore an
    option using the ROI manager, we will later explore another way
    using masks and image math. Select 'Nucleus' and 'Cell ROIs
    simultaneously. Then go to the \[More\>\>\] button and select the
    XOR operation. *XOR* is the *exclusive or* (exclusive disjunction).
    This is a logical operation that we apply to the ROIs. The XOR
    function returns the area where both inputs differ, i.e. not
    overlap. As the 'nucleus' ROI is located within the 'Cell' ROI, this
    subtracts the nucleus from the cell. Add the resulting ROI to the
    ROI Manager and rename to 'Cytoplasm'.

6.  Select all ROIs and save them to OMERO `[Plugin > OMERO > Save ROIs...]` - we will use these ROIs for
    measurements. Additionaly, you can save the ROIs to your local disk using the ROI manager. Do you recognize any advantages or disadvantages in saving ROIs to OMERO?
### tags: exercise roi-manager-1
\pagebreak
\newpage

## Using the ROI Manager 
Now, we are going to combine ROIs (and the ROI
Manager) with measurements -- you will see how powerful this already
gets!

1.  Open the image hela-cells.tif. Check the import ROIs option in the Bioformats options window or open the ROI Manager
    and load the previously generated ROI data.

2.  Measure the area and average intensity of the whole cell, the
    nucleus and the cytoplasm in the green channel and compare the
    results.

![Results window](fig/results-window.png){#fig:results-window width="65%"}   

3.  Create a ROI in the background of the image (no cell), select the
    green channel and measure the average intensity again. Name the ROI
    'Background' and update the saved ROI file; we will need this for
    further measurements.

### tags: exercise roi-manager-2
\pagebreak
\newpage
## Histogram Normalization

1.  Open the image hela-cells.tif and duplicate the green
    channel. Obtain a histogram.

2.  Use `[Process > Enhance Contrast]` on the duplicate. Set saturated
    pixels to 0, tick normalize and not equalize and obtain a histogram
    afterwards.

![Enhance contrast dialog](fig/enhance-contrast-dialog.png){#fig:enhance-contrast-dialog width="65%"}   

3.  Compare the histograms.

4.  Leave the images open; you can also explore different settings.
### tags: exercise histogram-2
\pagebreak
\newpage

## Subtracting background levels 
A common task is the subtraction of the
background levels of our images to make them comparable (background
levels might vary). Subtracting a constant is the most basic background
subtraction possible.

1.  Open the image hela-cells.tif and again check the load ROIs option to get your previously defined ROIs into the ROI manager.

2.  Measure the average intensity in the background and note the value.

3.  Select the overall image `[Edit > Selection > Select All]` in the
    green channel.

4.  Subtract the average background level from the green channel, using
    `[Process > Math > Subtract]`. You can also measure the backgrounds
    of the other color channels and subtract those as well.
### tags: exercise bg-subtraction-1
\pagebreak
\newpage

## Bit-depth/Format Problems 
Performing arithmetic operation changes the pixel values. This can potentially lead to e.g. clipped values. So where indicated care must be taken to convert images to a suitable bitdepth.

1.  Open the image hela-cells.tif. Duplicate the green
    channel.

2.  Look at the histogram of the green channel.

3.  Now, multiply the image by 2.5 - this increases the brightness of the image.

4.  Generate the histogram again and compare the number of saturated
    values. As you can see, if we get a value outside the image bit-depth the value will be clipped (i.e. set to the maximum value possible). If the result is a real
    number but our format only allows whole numbers, the resulting value is rounded. Of course, this was a rather stupid example, but
    this is a common mistake when you perform more complicated
    calculations on your images.

5.  Convert your image to an appropriate format and compare results.

### tags: exercise bitdepth-2
\pagebreak
\newpage

## Background subtraction 
In this example, we are exploring a common method
to subtract background information from a time-series. In the given
example, we have moving bacteria that were imaged with phase contrast
microscopy. The key idea for the background subtraction is that on each
pixel, most of the time no bacteria is visible. We therefore create an
average image and subtract this image from the original images to
increase contrast of moving bacteria.

1.  Open the image bacteria-tracks.tif. This image was
    create from supplementary video 1 of the publication: Rosser et
    al. (2013) Novel Methods for Analysing Bacterial Tracks Reveal
    Persistence in Rhodobacter sphaeroides, PLOS Computational Biology,
    DOI: 10.1371/journal.pcbi.1003276. Please note that this was not the
    original data, it seems that the supplementary movie was compressed!

2.  Perform a Z-projection to create an average image.

3.  Use `[Process > Image Calculator...]` to subtract the average image
    from each image in the original time-series and display the
    difference in a new window.

4.  Do you see any differences?

Not surprisingly, the authors of the original publication used exactly
this approach as the first step in their image processing.
### tags: exercise bg-subtracion-2
\pagebreak
\newpage

## Math on Masks 
Before, we used the ROI Manager XOR function to obtain the
cytoplasm ROI. We can obtain the same result using image masks and image
calculations (actually this is likely happening behind the scenes
anyway!).

1.  Open the image hela-cells.tif. Open the ROI Manager
    and load the previously generated ROI data that includes the
    background ROI.

2.  Duplicate just the green channel.

3.  Select the Nucleus ROI and create a mask (look at the previous
    exercise if you forgot how to proceed). Duplicate the mask.

4.  Now, select the Cell ROI and create another mask.

5.  You should now have two image masks (black-and-white images, see
    figure.

![Image masks](fig/image-masks.png){#fig:image-masks width="65%"}   

6.  Calculate the XOR function using the binary data of both images
    (`[Process > Image Calculator...]`).

7.  Compare the results with the cytoplasm ROI.

8.  Using `[Edit > Create Selection]`, you can create a selection from
    the mask.
### tags: exercise mask-1
\pagebreak
\newpage





## Background subtraction and batch processing 
To make this exercise more
interesting, we first establish the method we want to use and then apply
it to many files automatically. If a certain task is performed multiple
times, it is called *batch processing*.

1.  Open the image xu2015-adipocytes.tif. This image was
    provided as an example image by Elaine Xu (March 2015, Bruening lab,
    MPI Stoffwechselforschung). The image shows adipocytes and is a good
    example to illustrate uneven illumination and how to improve the
    image with background subtraction.

2.  At first, we explore a method to subtract the background. For this,
    we first perform a Gaussian blur on a duplicate image with a large
    $\sigma$ of $20$. This creates a very blurry image that already
    shows that we picked up the uneven illumination. You can look at a
    line profile in the original and the blurred image.

3.  Now we subtract the original image from the blurred image. Adjust
    brightness/contrast to confirm that background was subtracted. As
    the Gaussian blur is a low pass-filter, the subtraction of this
    low pass image can be considered as a (pseudo) high pass filtering.

4.  Fortunately, Fiji already has a function embedded that performs a
    similar operation for background subtraction, called a rolling ball
    background subtraction (Same idea: somehow calculate an average for
    every pixel. However, the actual calculations differ).

5.  We now want to perform the background subtraction on all image files
    in a certain folder. For this, we *record* our actions and then use
    the recorded sequence on each of those files.

6.  Close all images except the original xu2015-adipocytes.tif.

7.  To start the recording, perform `[Plugins > Macros > Record...]`. A
    Recorder window pops up (Fig.
    [\[fig:recorder-dialog\]](#fig:recorder-dialog){reference-type="ref"
    reference="fig:recorder-dialog"}). Make sure that 'Macro' is
    selected in Record and nothing else.

    [\[fig:recorder-dialog\]]{#fig:recorder-dialog
    label="fig:recorder-dialog"}

8.  Do `[Process > Subtract Background...]`, set the rolling ball radius
    to $20$ (Fig.
    [\[fig:rollingball-dialog\]](#fig:rollingball-dialog){reference-type="ref"
    reference="fig:rollingball-dialog"}). After you clicked on 'ok', the
    operation gets performed and the recorder should show following
    line: `run("Subtract Background...", "rolling=20");`.

    [\[fig:rollingball-dialog\]]{#fig:rollingball-dialog
    label="fig:rollingball-dialog"}

9.  Select the line and copy (Ctrl+C). Go to
    `[Process > Batch > Macro...]`. In the batch processing window,
    select the input folder /batch-files (please download from sciebo or OMERO). This folder
    contains 5 identical adipocyte images with different names. Also,
    choose an output folder, make sure that this output folder exists.
    Paste the line of code into the window (Fig.
    [\[fig:batch-process-dialog\]](#fig:batch-process-dialog){reference-type="ref"
    reference="fig:batch-process-dialog"}). and click on 'Process'.
    Check the chosen output folder for the results.

    [\[fig:batch-process-dialog\]]{#fig:batch-process-dialog
    label="fig:batch-process-dialog"}

When you try to perform a batch processing where a function requires
explicit file names the batch processor will fail because it does not
know that these need to be replaced (e.g. when the sequence Duplicate
Image, Gaussian, Image Calculator is used). In this case, we have to
create a macro where individual file names get replaced. 

### tags: exercise bg-subtraction-3 batch-1
\pagebreak
\newpage
## Working with Image Filters 


1.  Generate an 8-bit, 5x5 pixel black image with a white vertical line
    as shown in the convolution example. Duplicate and zoom in to
    observe individual pixels and check whether the intensity values of
    the black pixels are zero and the values of the white pixels
    are 255.

2.  Go to `[Process > Filters > Convolve...]`. Change the default kernel
    in the Convolver dialog to: $$\begin{array}{|c|c|c|}
        \hline
        1&1&1\\
    \hline
    1&1&1\\
    \hline
    1&1&1\\
    \hline
        \end{array}$$ Note that we did not enter 1/9; the values are
    automatically divided by the number of elements in the kernel if
    'Normalize Kernel' is ticked. Select 'Preview' if you directly want
    to observe the effects of your chosen kernel.

![Convolver dialog](fig/convolver-dialog.png){#fig:convolver-dialog width="45%"}   

\pagebreak
\newpage

3.  Compare the new pixel values with the values shown in the example.
    Do you observe any differences? You should note that pixels at the
    border of the image can show differences. This is caused by a
    different way to treat image borders. While the example simply
    ignores kernel positions outside the image, Fiji increases the image
    size to fit the kernel within the image (padding). These extra
    pixels are duplicates of border pixels and therefore, the results
    differ.
### tags: exercise filter-1

\pagebreak
\newpage

## The point spread function (PSF)

The image you obtain with a microscope is blurred by the optics of the
microscope itself. The point spread function describes the impulse
response of the microscope, i.e. the 3D diffraction pattern resulting
from a single point. In microscopes (non-coherent systems), the image
formation process is linear, which means that the imaging of many
objects produces a result that is the sum of individually imaged
objects. Therefore, image formation in a microscope can be seen as a
convolution of the true object with the PSF. Estimating the PSF of a
microscope then allows image deconvolution -- a process where the true
image is estimated by trying to reverse the effects of the convolution.
The problem is that deconvolution is an ill-posed problem -- no
solution, or no unique solution might exist and noise can strongly
influence a solution. Computing intense deconvolution algorithms are
used to approximate the true image; a PSF for deconvolution can be
obtained by measuring sub-resolution beads with know radii or by
theoretical estimation using parameters of the optical system.

In this exercise, we use an artificial ground-truth image and convolve
this image with a single slice of a cropped and low bit-depth version of
a measured PSF.

1.  Open the images artificial-groundtruth.tif and
    PSF-LeicaSP8-63x-Ar488.tif. The image shows a cropped,
    8 bit, x/y slice through a 3D PSF taken at the center (focal plane).

2.  Convolve the groundtruth image with the PSF by loading the file
    PSF-LeicaSP8-63x-Ar488.txt (the file is available on sciebo or as an attachment to the PSF image on OMERO) in the convolver dialog.

3.  Compare the groundtruth image with the convolved image. This is what
    happens every time you take an image with the microscope! (Although
    this is only a 2D, simplified example).
### tags: exercise filter-2
\pagebreak
\newpage

## Averaging pixels

1.  Open the image microtubuli.tif. Zoom into the image
    and observe the fluorescence fluctuations along the microtubuli.

2.  Preview the smoothing filter with a kernel size of 3x3 (see above),
    using `[Process > Filters > Convolve...]`. Then increase the kernel
    size to 5x5 and 7x7 and compare the results (duplicate the images!).
    What happens when the size of the kernel becomes larger? Can you
    enter a kernel size of 2x2?

3.  The averaging filter has its own direct command in Fiji. Go to
    `[Process > Filters > Mean...]`. You can choose a radius and
    optional preview in the next window. A radius can be given instead
    of size in X and Y as the kernel mask is circular -- the
    neighborhood can be defined arbitrarily! Circular kernels are common
    as pixels the outermost pixels have the same distance to the pixel
    of interest (Circular kernels can be shown with
    `[Process > Filters > Show Circular Masks...]`). Try different radii
    to obtain the best smoothing to suppress small fluorescence
    fluctuations.

4.  To show the effect of the filter more directly, you can subtract the
    smoothed from the original image.
### tags: exercise filter-3
\pagebreak
\newpage

## Gradient Filters

1.  Open the image microtubuli.tif. Zoom into the image
    and observe the fluorescence fluctuations along the microtubuli.
    Remember to duplicate the images before testing any processing.

2.  At first, test the sharpen filter with `[Process > Sharpen]` and
    optionally using the kernel in the convolution dialog.

3.  The find edge filter can be tested directly using
    `[Process > Find Edges]`. If you want to explore the filter a bit
    more, you can also generate both filtered images, convert those to
    32 bit and perform the calculations by yourself. Are the results
    identical?

4.  What happens to the noise if you use the sharpen filter?

5.  What happens if you first use a smoothing filter and then the edge
    detection filter?
### tags: exercise filter-4
    \pagebreak
\newpage

## Gaussian Filters

1.  Open the image microtubuli.tif. Zoom into the image
    and observe the fluorescence fluctuations along the microtubuli.
    Remember to duplicate the images before testing any processing.

2.  The gaussian filter can be tested using
    `[Process > Filters > Gaussian Blur...]`.

3.  Try to find an optimal value for $\sigma$.

4.  Implement a DoG filter with $\sigma$ values of $1$ and $10$.
### tags: exercise filter-5
\pagebreak
\newpage

## Median Filter

1.  Open the image microtubuli.tif. Before we do any
    further processing, we add some Salt-and-Pepper noise using
    `[Process > Noise > Salt and Pepper]`. This sets random pixels to
    the lowest or highest values.

2.  Duplicate the image with added noise and perform the mean filter to
    suppress the just added noise (find a suitable radius).

3.  Now, use the median filter `[Process > Filters > Median]` with the
    same radius.

4.  Which filter works better?
### tags: exercise filter-6

\pagebreak
\newpage



## Thresholding with contrast adjustment 
Let us first have a look at the
effects of thresholding using brightness/contrast adjustments.

1.  Open the image cell-colony.tif Open the
    brightness/contrast adjustment window. Observe the slope of the line
    that shows the change in (displayed) intensity between the minimum
    and maximum pixel values in the histogram.

![Brightness and Contrast](fig/bc-window1.png){#fig:bc-window1 width="35%"}   


2.  Now, set the contrast to the maximum value and observe that the
    slope of the line changes until the line appears nearly vertical.
    The image is a black and white image now, everything to the left of
    the line is black, everything right of the line is white (the
    majority of the pixels as seen in the histogram).

3.  If you now change the brightness, you can move this vertical line
    around and observe that the number of pixels identified as white
    (black) changes.
### tags: exercise  
\pagebreak
\newpage

## Manual thresholding 
Instead of adjusting the contrast, Fiji has a
specialized function to adjust the threshold
`[Image > Adjust > Threshold...]`.

1.  Open the image cell-colony.tif if it is not already
    open.

2.  Do `[Image > Adjust > Threshold...]` to open the threshold
    adjustment window. In this window, you can
    set the intensity for the threshold. Furthermore, you can select
    whether you have a dark or light background to determine whether you
    are interested in light or dark objects. Note that you can select a
    window for your threshold, by setting the lower and upper values to
    a value outside the extremes. This is called a *density slice* and
    can be used to detect objects that fall within a certain intensity
    range.


![Adjust threshold](fig/adjust-threshold-dialog.png){#fig:adjust-threshold-dialog width="35%"}   


3.  Change values and play with different settings until you think you
    found an optimal threshold. How difficult is it to obtain an optimal
    threshold, i.e. how sensitive is the result to your chosen value?
### tags: exercise threshold-1
\pagebreak
\newpage
## Automated thresholding

1.  Open the image hela-cells.tif. In this task, we first
    want to automatically identify the nuclei. Select the appropriate
    channel and duplicate.

2.  Test all available thresholding methods. You can see that most
    method already produce very nice results.

3.  In the next step, we want to identify the lysosomes (red). Try to
    threshold the appropriate channel with Otsu's method. Are the
    results good enough?

4.  As you can see, the algorithm already works relatively well, but is
    not good enough for our purposes. Can you think of a reason why the
    method fails in some parts of the cells?

5.  After an analysis, we come to the conclusion that background signal
    is too high in parts of the cell. Therefore, we now first use a
    background subtraction (e.g. with a rolling ball radius of 10
    pixels) before we threshold with Otsu's method. Do the results
    improve?

6.  Finally, try to use the green channel to identify the cells'
    cytoplasm. Again, it seems that an image filter might improve the
    results. Try a Gaussian filter with varying sigma values to improve
    the results. At the end, the result we obtain is not perfect but
    might be sufficient for our needs. You will see in the section about
    binary images how we could still improve on this thresholding.
### tags: exercise threshold-2
\pagebreak
\newpage
## Morphological operations

1.  Open the image thresholded-nuclei.tif. This image
    shows real thresholded nuclei with artificially introduced
    thresholding errors.

2.  Perform erosion, dilation, opening and closing in
    `[Process > Binary]` and observe the changes of individual nuclei.
    Make sure you understand where the different operations enhance the
    image and where they make analysis more difficult.

3.  Instead of using opening or closing, try to manually erode 4-5 times
    and then dilate 4-5 times again; perform the same operations
    reversed.

4.  Try the command `[Process > Binary > Fill Holes]`. This operation
    finds background areas that are completely surrounded by foreground
    and sets all those pixels to foreground.
### tags: exercise morphology-1   
\pagebreak
\newpage

## Skeleton analysis

1.  Open the image drosophila-ddac-neuron.tif. In this
    task, you are going to analyze the arborization pattern of this,
    already thresholded, neuron.

2.  Duplicate the image, do
    `[Plugins > Skeleton > Skeletonize (2D/3D)]`. Make sure that the
    skeleton is white against a black background (you might need to
    invert the image). Now, edit the LUT so that the white pixels appear
    yellow, magenta or any other light color.

3.  Look at the original thresholded image and add the skeletonized
    image as an overlay (with zero transparent). Analyze the
    skeletonization results with the overlay.

4.  Perform `[Analyze > Skeleton > Analyze Skeleton (2D/3D)]` on the
    skeletonized image. The Analyze Skeleton window allows you to prune
    the skeleton before analysis to get rid of small branches either by
    their length or intensity. Tick 'Show detailed info' and click on
    'OK'.

![Analyze skeleton dialog](fig/analyze-skeleton-dialog.png){#fig:analyze-skeleton-dialog width="35%"}   


5.  Three windows show up: Detailed information about each branch,
    summary results with branch statistics, and an image showing the
    skeleton with branch points and end points in different colors. You
    can try out different prune methods and compare the results. Refer to https://imagej.net/AnalyzeSkeleton to get more information on the visualization.
### tags: exercise morphology-2
\pagebreak
\newpage

## Watershed transform

1.  Open the image bunch-of-nuclei.tif. Use the
    gauss-filter and thresholding to generate a binary image with the
    nuclei detected. Duplicate.

2.  Use `[Process > Binary > Watershed]` on the binary image. Observe
    where the algorithm splits objects.
### tags: exercise watershed-1
\pagebreak
\newpage

## Analyze Particles

1.  Open the image bunch-of-nuclei.tif and use a sequence
    of filtering, thresholding and binary operations to identify the
    nuclei. Remember that this image does not provide an easy perfect
    result on purpose!

2.  Set the measurements you want to perform
    `[Analyze > Set Measurements...]`. For this example, we want at
    least measure the area and the mean gray value.

3.  Perform `[Analyze > Analyze Particles...]`. Do not select objects by
    size or circularity, show the outlines and tick 'Display results',
    'Clear results', 'Add to Manager' and 'Summarize'.

4.  Several windows should show up. A summary report indicating the
    number of detected objects, and several average statistics; A
    results window showing the selected measurements for each detected
    object; an outline image indicating the object number for each
    object; the ROI Manager with each object as an individual ROI. Why
    is the mean intensity value $255$ for each object? The measurement
    was performed on the thresholded binary image. While thresholding
    does not change the shape of an object, the intensity values are
    obviously not maintained. In order to perform the measurements on
    the original image, Redirect the measurements to the original image
    in 'Set Measurements\...'.

5.  Explore the functions of the particle-analyzer method and try to
    select objects in a way that only small/large or round objects are
    measured.
### tags: exercise particle-analyzer-1
\pagebreak
\newpage

# Part 3


## Trainable Weka Segmentation

1.  Open the image 1546 Ctr3G-KO1R 24h.lif, which was kindly provided by Matthias Rübsam. It shows a mixture of two different populations of primary ceratinocytes labelled with green and red fluorescent markers. The nuclei are stained with a Hoechst dye. Select a rectangular ROI which includes about 20-30 nuclei and duplicate the blue channel. Save the image as segmentation-challenge.tif.

2. Manually count the nuclei in the image using the Multi-point tool. Exclude nuclei which touch the border.

3. Quickly try to do a segmentation using a manual threshold and watershed operation. Count the number of nuclei using the particle analyzer (exclude on edges as well).

4.  Now start again from segmentation-challenge.tif file. Go to `[Plugins > Segmentation > Trainable Weka Segmentation]`. A window pops up that shows the image and several buttons.

![Trainable WEKA segmentation](fig/weka-segmentation-window.png){#fig:weka-segmentation-window width="65%"}   


3.  Use the freehand line tool and draw on an image object you want to
    detect. Add this selection to class 1. Repeat this step and then add
    two background selections to class 2.

4.  Click on 'Train classifier'. You should now see what the method
    thinks is background and foreground. If you click on 'Create result'
    a two color image is generated. Convert this image into a
    binary image, perform a watershed operation and count nuclei again.
### tags: exercise weka-1

## StarDist Segmentation

1.   Go to `[Help > Update]`, then click ¨Manage update sites¨. Check the sites CSBDeep and StarDist. Click the ¨Close¨ button and ¨Apply changes¨. It may take a while to download. After it finished please restart FIJI.

2. Open segmentation-challenge.tif and open StarDist segmentation via the menu `[Plugins > Stardist > StarDist 2D]`, keep the default settings and run stardist by clicking the ¨OK¨ button.

3. Compare your results.

4. Run the Stardist segmentation again and explore the effect of different settings (e.g. Probability/ Score Threshold and Overlap Threshold).

5. Refer to https://imagej.net/StarDist for further information. Be aware that you are employing a pre-trained model here which may well be not applicable to your data and produce non-sense results. However, if you have labelled training data your can train you Stardist model perfectly adapted to your data.
### tags: exercise stardist