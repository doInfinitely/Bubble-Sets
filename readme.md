
This is an implementation of [bubble sets] [1]
without the use of external libraries.

To build the project, you can use the ANT-script
provided by build.xml - it generates two jars with
their respective sources in zip files.

The jar example.jar contains a little example
program showing off the bubble sets. The other
jar, bubbleset.jar, contains the api for the
bubble sets.

To get started, you can use the following code:

    // a list of groups of rectangles --
    // bubble set will try to create an outline with
    // as little overlap between the groups as possible
    List<Rectangle2D[]> items = ...;

    // using bubble set outlines
    SetOutline setOutline = new BubbleSet();

    // make the outlines smooth
    AbstractShapeCreator shapeCreator = new BezierShapeGenerator(setOutline);

    // generate shapes for each group
    // the shapes can be drawn by a Graphics object
    // as passed by a component's paint method
    Shape[] shapes = shapeCreator.createShapesFor(items);

A more advanced example uses groups which can also
define lines that guide the iso-contour. It also shows
a possible use within a paint method:

    @Override
    public void paint(final Graphics gfx) {
        // using graphics 2d
        Graphics2D g = (Graphics2D) gfx;

        // the list of groups
        List<Group> items = null;

        // make the outlines smooth and use bubble sets
        AbstractShapeCreator shapeCreator = new BezierShapeGenerator(new BubbleSet());

        // generate shapes for each group
        Shape[] shapes = shapeCreator.createShapesForGroups(items);

        for (Shape shape : shapes) {
            // drawing the content
            g.setColor(Color.ORANGE);
            g.fill(shape);
            
            // and then the outlines
            g.setColor(Color.BLACK);
            g.draw(shape);
        }
    }

[1]: http://faculty.uoit.ca/collins/research/bubblesets/ "Collins, Christopher; Penn, Gerald; Carpendale, Sheelagh. Bubble Sets: Revealing Set Relations over Existing Visualizations. In IEEE Transactions on Visualization and Computer Graphics (Proceedings of the IEEE Conference on Information Visualization (InfoVis '09)), 15(6): November-December, 2009."
