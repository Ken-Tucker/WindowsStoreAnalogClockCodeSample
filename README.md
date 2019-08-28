#Introduction
Create a Analog Clock in a windows store application

#Building the Sample
You can build this application with Visual Studio 2013 on a computer using Windows 8.1 as the operating system

#Description

This sample uses xaml and c# to create an analog clock in a windows store application.  Xaml allows you to vary the angle of lines when drawn on the screen. I used an ellipse as the background of the clock. We will draw 3 lines for the hour, seconds, and minute hand on an analog clock.  A rotate transform turns a line into the second, minute and hour hand.  The transform will draw the line from the center of a circle at the angle needed to represent the time. For seconds and minutes multiply the value by 6 to get the angle for the clocks hand transform.  For hours multiply the hour by 30 to get the angle needed for the hour hand transform.   I use a dispatch timer to update angle of the hands based on the current time.  The dispatch timer will fire an event every second which we use to update the angle of the clocks hand.   The clock could be improved by using a clock image instead of an ellipse.  

Additional work would need to be done to be able to submit the app to the store.   If ads were added you would need to give the app permission to access the internet.  Any app that has access to the internet would require a privacy policy.

 

Sample updated to work with windows 8.1 and vs 2013 on 12/24/2013. Also included a Visual Basic version

'''Visual Basic
   Dim timer As New DispatcherTimer 
 
 
    Public Sub New() 
 
        ' This call is required by the designer. 
        InitializeComponent() 
 
        ' Add any initialization after the InitializeComponent() call. 
        timer.Interval = TimeSpan.FromSeconds(1) 
        AddHandler timer.Tick, AddressOf Timer_Tick 
 
        timer.Start() 
    End Sub 
 
    Public Sub Timer_Tick(sender As Object, e As EventArgs) 
        secondHand.Angle = DateTime.Now.Second * 6 
        minuteHand.Angle = DateTime.Now.Minute * 6 
        hourHand.Angle = (DateTime.Now.Hour * 30) + (DateTime.Now.Minute * 0.5) 
    End Sub
    
    
    
    '''c#
        DispatcherTimer timer = new DispatcherTimer(); 
 
        public MainPage() 
        { 
            this.InitializeComponent(); 
            timer.Interval = TimeSpan.FromSeconds(1); 
            timer.Tick += timer_Tick; 
            timer.Start();  
        } 
         
        void timer_Tick(object sender, object e) 
        { 
            secondHand.Angle = DateTime.Now.Second * 6; 
            minuteHand.Angle = DateTime.Now.Minute * 6; 
            hourHand.Angle = (DateTime.Now.Hour * 30) + (DateTime.Now.Minute * 0.5); 
        }
        
        
        
    '''XAML
       <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}"> 
        <Grid Width="300" Height="300"> 
            <Ellipse Width="300" Height="300" Fill="Blue"></Ellipse> 
            <!-- Second  --> 
            <Rectangle Margin="150,0,149,150" Name="rectangleSecond"  
        Stroke="White" Height="120" VerticalAlignment="Bottom"> 
                <Rectangle.RenderTransform> 
                    <RotateTransform x:Name="secondHand" CenterX="0"  
                CenterY="120" Angle="0" /> 
                </Rectangle.RenderTransform> 
            </Rectangle> 
            <!----> 
         
        <!-- Minute  --> 
            <Rectangle Margin="150,49,149,151" Name="rectangleMinute"  
        Stroke="LightGreen"> 
                <Rectangle.RenderTransform> 
                    <RotateTransform x:Name="minuteHand" CenterX="0"  
                CenterY="100" Angle="0" /> 
                </Rectangle.RenderTransform> 
            </Rectangle> 
            <!----> 
         
        <!-- Hour  --> 
            <Rectangle Margin="150,80,149,150" Name="rectangleHour"  
        Stroke="LightYellow"> 
                <Rectangle.RenderTransform> 
                    <RotateTransform x:Name="hourHand" CenterX="0"  
                CenterY="70" Angle="0" /> 
                </Rectangle.RenderTransform> 
            </Rectangle> 
            <!----> 
         
    </Grid> 
    </Grid>
