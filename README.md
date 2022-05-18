
/Ivana Pejicic
//Chapter 11, Challenge #10
//Slot Machine Simulation Challenge
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.paint.Color;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.VBox;
import javafx.scene.control.Label;
import javafx.scene.control.Button;
import javafx.event.EventHandler;
import javafx.event.ActionEvent;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.shape.*;

import java.util.Random;

public class SlotMachineSimulation extends Application
{
    VBox col1, col2, col3;
    HBox row1,row2;
    TextField amount;
    int total = 0;
    ImageView view1, view2, view3;
    Label wonSpin, wonTotal;

    public static void main(String[] args)
    {
       launch(args);
    }
    public void start(Stage primaryStage)
    {
        primaryStage.setTitle("SLOT MACHINE");

        GridPane gridPane = new GridPane();
        gridPane.setPadding(new Insets(10,50,50,50));

        gridPane.setHgap(10);
        gridPane.setVgap(12);

        row1 = new HBox(10);
        row2 = new HBox(10);

        gridPane.add(row1, 0,0);
        gridPane.add(row2, 0,1);

        Rectangle rectangle = new Rectangle(10,10,180,60);
        row1.getChildren().addAll(rectangle);

        col1 = new VBox(10);
        col2 = new VBox(10);
        col3 = new VBox(10);

        col1.setPadding(new Insets(10,10,10,10));
        col2.setPadding(new Insets(10,10,10,10));
        col3.setPadding(new Insets(10,10,10,10));
        row2.getChildren().addAll(col1,col2,col3);

        Button button = new Button();
        button.setText("SPIN");

        Label label = new Label ("Amount Inserted:");
        amount = new TextField();
        wonSpin = new Label("Won for this spin: ");
        wonTotal = new Label("Total won: ");

        Label message = new Label ("Please enter amount: ");
        message.setVisible(false);

        col1.getChildren().addAll(label, amount, message);
        col2.getChildren().addAll(button);
        col3.getChildren().addAll(wonSpin, wonTotal);

        primaryStage.setScene(new Scene(gridPane, 550, 300));
        primaryStage.show();

        button.setOnAction(new EventHandler<ActionEvent>()
        {
            public void handle(ActionEvent event)
            {
                message.setVisible(false);
                try
                {
                    int spinAmount = Integer.parseInt(amount.getText());
                    Random rand = new Random();
                    DisplayCalculate(rand.nextInt(3)+1, rand.nextInt(3)+1, rand.nextInt(3)+1, spinAmount);
                }
                catch(NumberFormatException e)
                {
                    message.setVisible(true);
                }
            }
        });



   }
   public void DisplayCalculate(int random1, int random2, int random3, int spinAmount)
   {
       row1.getChildren().clear();
       String path = "/images/" + random1 + ".jpg";
       Image image = new Image (path);
       view1 = new ImageView(image);
       row1.getChildren().addAll(view1);

       path = "/images/" + random2 + ".jpg";
       image = new Image (path);
       view2 = new ImageView(image);
       row1.getChildren().addAll(view2);

       path = "/images/" + random3 + ".jpg";
       image = new Image (path);
       view3 = new ImageView(image);
       row1.getChildren().addAll(view3);

       view1.setFitHeight(60);
       view1.setFitWidth(60);
       view2.setFitHeight(60);
       view2.setFitWidth(60);
       view3.setFitHeight(60);
       view3.setFitWidth(60);

       if (random1 == random2 && random1 == random3)
       {
           spinAmount = spinAmount * 3;
       }
       else if (random1 == random2 || random1 == random3 || random2 == random3)
       {
           spinAmount = spinAmount * 2;
       }
       else
           spinAmount = 0;

       total = total + spinAmount;
       wonSpin.setText("Won for this spin: $" + spinAmount);
       wonTotal.setText("Total won: $" + total);
   }
   public int getRandomInteger (int maximum, int minimum)
   {
       return ((int) (Math.random()*(maximum-minimum))) + minimum;
   }
}
