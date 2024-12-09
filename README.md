# Lab-Assignment-vp-
<Window x:Class="CricketTeamManager.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Cricket Team Manager" Height="400" Width="400">
    <Grid Margin="10">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>

        <TextBlock Text="Cricket Team Manager" 
                   FontSize="24" 
                   HorizontalAlignment="Center" 
                   Margin="0,0,0,10"/>
        
        <StackPanel Grid.Row="1" Orientation="Horizontal" HorizontalAlignment="Center" Margin="0,10,0,10">
            <TextBox x:Name="playerNameTextBox" Width="200" Height="30" Margin="0,0,10,0" VerticalContentAlignment="Center"/>
            <Button x:Name="addPlayerButton" Content="Add Player" Width="100" Height="30" Click="AddPlayerButton_Click"/>
        </StackPanel>

        <StackPanel Grid.Row="2" Margin="0,10,0,0">
            <ListBox x:Name="playerListBox" Height="200" Margin="0,0,0,10" FontSize="14"/>
            <Button x:Name="removePlayerButton" Content="Remove Player" Height="30" Click="RemovePlayerButton_Click"/>
        </StackPanel>
    </Grid>
</Window>



using System.Collections.ObjectModel;
using System.Windows;

namespace CricketTeamManager
{
    public partial class MainWindow : Window
    {
        // ObservableCollection to hold the player names
        private ObservableCollection<string> players;

        public MainWindow()
        {
            InitializeComponent();

            // Initialize the players list
            players = new ObservableCollection<string>();
            playerListBox.ItemsSource = players; // Bind ListBox to ObservableCollection
        }

        // Event handler for adding a player
        private void AddPlayerButton_Click(object sender, RoutedEventArgs e)
        {
            string playerName = playerNameTextBox.Text.Trim();

            if (string.IsNullOrEmpty(playerName))
            {
                MessageBox.Show("Player name cannot be empty!", "Error", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            if (players.Contains(playerName))
            {
                MessageBox.Show("Player name already exists!", "Error", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            players.Add(playerName);
            playerNameTextBox.Clear();
            MessageBox.Show($"Player '{playerName}' added successfully!", "Success", MessageBoxButton.OK, MessageBoxImage.Information);
        }

        // Event handler for removing a player
        private void RemovePlayerButton_Click(object sender, RoutedEventArgs e)
        {
            string selectedPlayer = playerListBox.SelectedItem as string;

            if (string.IsNullOrEmpty(selectedPlayer))
            {
                MessageBox.Show("No player selected!", "Error", MessageBoxButton.OK, MessageBoxImage.Warning);
                return;
            }

            players.Remove(selectedPlayer);
            MessageBox.Show($"Player '{selectedPlayer}' removed successfully!", "Success", MessageBoxButton.OK, MessageBoxImage.Information);
        }
    }
}
