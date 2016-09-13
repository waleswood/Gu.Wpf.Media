# Gu.Wpf.Media
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE.md) 
[![NuGet](https://img.shields.io/nuget/v/Gu.Wpf.Media.svg)](https://www.nuget.org/packages/Gu.Wpf.Media/)
[![Build status](https://ci.appveyor.com/api/projects/status/a92oxrywc9nv7f21?svg=true)](https://ci.appveyor.com/project/JohanLarsson/gu-wpf-numericinput)

Wrapper for System.Windows.Controls.MediaElement.

# Contents

# 1. Properties
The wrapper wraps the properties of System.Windows.Controls.MediaElement and adds a couple of new properties.
Mapped properties are dependency properties that are updated when needed.

## 1.1. State (`MediaState`)
The current `MediaState` of the player.

## 1.2. Position (`Timespan?`)
The current position in the media, `null` if no media is loaded.
Twoway bindable and updates every 0.1 s when playing.

## 1.3. Length (`Timespan?`)
The length of the current media, `null`if no media is loaded.

## 1.4. CanPauseMedia (`bool?`)
Mapped to System.Windows.Controls.MediaElement.CanPause, `null`if no media is loaded.

## 1.5. NaturalVideoHeight (`int?`)
Mapped to System.Windows.Controls.MediaElement.NaturalVideoHeight, `null`if no media is loaded.

## 1.6. NaturalVideoWidth (`int?`)
Mapped to System.Windows.Controls.MediaElement.NaturalVideoWidth, `null`if no media is loaded.

## 1.7. HasAudio (`bool?`)
Mapped to System.Windows.Controls.MediaElement.HasAudio, `null`if no media is loaded.

## 1.8. HasVideo (`bool?`)
Mapped to System.Windows.Controls.MediaElement.HasVideo, `null`if no media is loaded.

## 1.9. SpeedRatio (`double`)
Mapped to System.Windows.Controls.MediaElement.SpeedRatio.

## 1.10. IsBuffering (`bool`)
Mapped to System.Windows.Controls.MediaElement.IsBuffering.

## 1.11. DownloadProgress (`double`)
Mapped to System.Windows.Controls.MediaElement.DownloadProgress.
Updated every 1 s when buffering.

## 1.12. BufferingProgress (`double`)
Mapped to System.Windows.Controls.MediaElement.BufferingProgress.
Updated every 1 s when buffering.

## 1.13. VolumeIncrement (`double`)
How much volume is changed when MediaCommands.IncreaseVolume & MediaCommands.DecreaseVolume are invoked.
Default 0.05;

## 1.14. VideoFormats
A list of video file formats for convenience.
*.dat; *.wmv; *.3g2; *.3gp; *.3gp2; *.3gpp; *.amv; *.asf;  *.avi; *.bin; *.cue; *.divx; *.dv; *.flv; *.gxf; *.iso; *.m1v; *.m2v; *.m2t; *.m2ts; *.m4v; *.mkv; *.mov; *.mp2; *.mp2v; *.mp4; *.mp4v; *.mpa; *.mpe; *.mpeg; *.mpeg1; *.mpeg2; *.mpeg4; *.mpg; *.mpv2; *.mts; *.nsv; *.nuv; *.ogg; *.ogm; *.ogv; *.ogx; *.ps; *.rec; *.rm; *.rmvb; *.tod; *.ts; *.tts; *.vob; *.vro; *.webm

Usage:

```c#
OpenFileDialog openFileDialog = new OpenFileDialog
{
    Filter = $"Media files|{this.MediaElement.VideoFormats}|All files (*.*)|*.*"
};

if (openFileDialog.ShowDialog() == true)
{
    this.MediaElement.Source = new Uri(openFileDialog.FileName);
}
```

## 1.15. AudioFormats
A list of audio file formats for convenience.
*.mp3; *.wma; *.aac; *.adt; *.adts; *.m4a; *.wav; *.aif; *.aifc; *.aiff; *.cda

Usage:

```c#
OpenFileDialog openFileDialog = new OpenFileDialog
{
    Filter = $"Media files|{this.MediaElement.AudioFormats}|All files (*.*)|*.*"
};

if (openFileDialog.ShowDialog() == true)
{
    this.MediaElement.Source = new Uri(openFileDialog.FileName);
}
```

## 1.16. Source (`Uri`)
Mapped to System.Windows.Controls.MediaElement.Source.
When source changes play is invoked to trigger load. Then pause is invoked in the MediaOpened event.
This results in the video paused at the first frame as initial state after setting `Source`
Subscribe to `MediaOpened` if you want to start playing on load.

## 1.17. Volume (`double`)
Mapped to System.Windows.Controls.MediaElement.Volume.

## 1.18. Balance (`double`)
Mapped to System.Windows.Controls.MediaElement.Balance.

## 1.19. IsMuted (`bool`)
Mapped to System.Windows.Controls.MediaElement.IsMuted.

## 1.20. ScrubbingEnabled (`bool`)
Mapped to System.Windows.Controls.MediaElement.ScrubbingEnabled.

## 1.21. Stretch (`Stretch`)
Mapped to System.Windows.Controls.MediaElement.Stretch.

## 1.22. StretchDirection (`StretchDirection`)
Mapped to System.Windows.Controls.MediaElement.StretchDirection.

# 2. Events

## 2.1. MediaFailed
Mapped to System.Windows.Controls.MediaElement.MediaFailed.

## 2.2. MediaOpened
Mapped to System.Windows.Controls.MediaElement.MediaOpened.

## 2.3. BufferingStarted
Mapped to System.Windows.Controls.MediaElement.BufferingStarted.

## 2.4. BufferingEnded
Mapped to System.Windows.Controls.MediaElement.BufferingEnded.

## 2.5. ScriptCommand
Mapped to System.Windows.Controls.MediaElement.ScriptCommand.

## 2.6. MediaEnded
Mapped to System.Windows.Controls.MediaElement.MediaEnded.

# 3. MediaCommands
Adds command bindings for:
  - MediaCommands.Play
  - MediaCommands.Pause
  - MediaCommands.Stop
  - MediaCommands.TogglePlayPause
  - MediaCommands.Rewind
  - MediaCommands.IncreaseVolume
  - MediaCommands.DecreaseVolume
  - MediaCommands.MuteVolume




# 4. Sample

```xaml
<UserControl.CommandBindings>
    <CommandBinding Command="ApplicationCommands.Open" Executed="OpenExecuted" />
</UserControl.CommandBindings>
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
        <RowDefinition Height="Auto" />
    </Grid.RowDefinitions>
    <ToolBar>
        <Button Command="ApplicationCommands.Open">
            Open
        </Button>
        <Separator />

        <Button Command="MediaCommands.Play" CommandTarget="{Binding ElementName=MediaElement}">
            Play
        </Button>
        <Button Command="MediaCommands.Pause" CommandTarget="{Binding ElementName=MediaElement}">
            Pause
        </Button>
        <Button Command="MediaCommands.Stop" CommandTarget="{Binding ElementName=MediaElement}">
            Stop
        </Button>
    </ToolBar>

    <media:MediaElementWrapper x:Name="MediaElement"
                                Grid.Row="1"
                                ScrubbingEnabled="True" />

    <StatusBar Grid.Row="2">
        <StatusBar.ItemsPanel>
            <ItemsPanelTemplate>
                <Grid>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="*" />
                        <ColumnDefinition Width="Auto" />
                    </Grid.ColumnDefinitions>
                </Grid>
            </ItemsPanelTemplate>
        </StatusBar.ItemsPanel>

        <StatusBarItem Grid.Column="0" HorizontalContentAlignment="Stretch">
            <Slider x:Name="ProgressSlider"
                    Maximum="{Binding ElementName=MediaElement,
                                        Path=Length,
                                        Converter={x:Static local:TimeSpanToSecondsConverter.Default}}"
                    Minimum="0"
                    Thumb.DragCompleted="OnProgressSliderDragCompleted"
                    Thumb.DragStarted="OnProgressSliderDragStarted"
                    Value="{Binding ElementName=MediaElement,
                                    Path=Position,
                                    Converter={x:Static local:TimeSpanToSecondsConverter.Default}}" />
        </StatusBarItem>

        <StatusBarItem Grid.Column="1">
            <TextBlock>
                <TextBlock.Text>
                    <MultiBinding StringFormat="{}{0}/{1}">
                        <Binding ElementName="MediaElement" Path="Position" />
                        <Binding ElementName="MediaElement" Path="Length" />
                    </MultiBinding>
                </TextBlock.Text>
            </TextBlock>
        </StatusBarItem>
    </StatusBar>
</Grid>
```

With code behind:

```c#
public partial class MediaElementWrapperView : UserControl
{
    private MediaState mediaState;

    public MediaElementWrapperView()
    {
        this.InitializeComponent();
    }

    private void OpenExecuted(object sender, ExecutedRoutedEventArgs e)
    {
        OpenFileDialog openFileDialog = new OpenFileDialog
        {
            Filter = $"Media files|{this.MediaElement.VideoFormats}|All files (*.*)|*.*"
        };

        if (openFileDialog.ShowDialog() == true)
        {
            this.MediaElement.Source = new Uri(openFileDialog.FileName);
        }
    }

    private void OnProgressSliderDragStarted(object sender, DragStartedEventArgs e)
    {
        this.mediaState = this.MediaElement.State;
        this.MediaElement.Pause();
    }

    private void OnProgressSliderDragCompleted(object sender, DragCompletedEventArgs e)
    {
        this.MediaElement.Position = TimeSpan.FromSeconds(this.ProgressSlider.Value);
        if (this.mediaState == MediaState.Play)
        {
            this.MediaElement.Play();
        }
    }
}
```

Check out the demo project for more samples.

