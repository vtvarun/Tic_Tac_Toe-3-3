# Tic_Tac_Toe-3-3
It's a classical two players game where the objective is to fill any row or any column or any diagonal with the  x's or o's.

Code : 
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package com.example.tictactoepractise2;

import java.io.IOException;
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Node;
import javafx.scene.Scene;
import javafx.scene.control.Alert;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.Alert.AlertType;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.stage.Stage;

public class HelloApplication extends Application {
    Label scoreBoard1;
    Label scoreBoard2;
    int playerXScore = 0;
    int playerOScore = 0;
    boolean turn = true;
    private Button[][] buttons = new Button[3][3];

    public HelloApplication() {
    }

    public BorderPane createPane() {
        BorderPane root = new BorderPane();
        root.setPadding(new Insets(20.0, 20.0, 20.0, 20.0));
        Label title = new Label("Tic-Tac-Toe");
        title.setStyle("-fx-font-size : 25pt;");
        BorderPane.setAlignment(title, Pos.CENTER);
        root.setTop(title);
        GridPane grid = new GridPane();
        grid.setHgap(10.0);
        grid.setVgap(10.0);

        for(int col = 0; col < 3; ++col) {
            for(int row = 0; row < 3; ++row) {
                Button newButton = new Button("");
                newButton.setPrefSize(200.0, 200.0);
                newButton.setStyle("-fx-font-size : 50pt");
                newButton.setOnAction((actionEvent) -> {
                    this.click(newButton);
                });
                this.buttons[col][row] = newButton;
                grid.add(newButton, col, row);
            }
        }

        root.setCenter(grid);
        grid.setAlignment(Pos.CENTER);
        this.scoreBoard1 = new Label("Player X : " + this.playerXScore);
        this.scoreBoard2 = new Label("Player Y : " + this.playerOScore);
        this.scoreBoard1.setStyle("-fx-font-size : 24pt");
        this.scoreBoard2.setStyle("-fx-font-size : 24pt");
        HBox hbox = new HBox();
        hbox.getChildren().addAll(new Node[]{this.scoreBoard1, this.scoreBoard2});
        hbox.setSpacing(300.0);
        root.setBottom(hbox);
        hbox.setAlignment(Pos.CENTER);
        return root;
    }

    public void start(Stage stage) throws IOException {
        Scene scene = new Scene(this.createPane());
        stage.setTitle("Tic-Tac-Toe-P2");
        stage.setScene(scene);
        stage.show();
    }

    private void click(Button button) {
        if (button.getText().equals("")) {
            if (this.turn) {
                button.setText("X");
            } else {
                button.setText("O");
            }

            this.turn = !this.turn;
            this.checkWinner();
            this.allButtonsCliked();
        }

    }

    private void allButtonsCliked() {
        boolean allClicked = true;

        for(int i = 0; i < 3; ++i) {
            for(int j = 0; j < 3; ++j) {
                if (this.buttons[i][j].getText().isEmpty()) {
                    allClicked = false;
                }
            }
        }

        if (allClicked) {
            Alert alert = new Alert(AlertType.INFORMATION);
            alert.setTitle("Draw");
            alert.setContentText("Click 'OK' to play next round");
            alert.setHeaderText("");
            alert.showAndWait();
            this.restart();
        }

    }

    private void updateScore(String winner) {
        if (winner.equals("X")) {
            ++this.playerXScore;
            this.scoreBoard1.setText("Player X : " + this.playerXScore);
        } else {
            ++this.playerOScore;
            this.scoreBoard2.setText("Player O : " + this.playerOScore);
        }

    }

    private void checkWinner() {
        int col;
        for(col = 0; col < 3; ++col) {
            if (this.buttons[0][col].getText().equals(this.buttons[1][col].getText()) && this.buttons[0][col].getText().equals(this.buttons[2][col].getText()) && !this.buttons[0][col].getText().isEmpty()) {
                this.updateScore(this.buttons[0][col].getText());
                this.displayWinner(this.buttons[0][col].getText());
            }
        }

        for(col = 0; col < 3; ++col) {
            if (this.buttons[col][0].getText().equals(this.buttons[col][1].getText()) && this.buttons[col][0].getText().equals(this.buttons[col][2].getText()) && !this.buttons[col][0].getText().isEmpty()) {
                this.updateScore(this.buttons[col][0].getText());
                this.displayWinner(this.buttons[col][0].getText());
            }
        }

        if (this.buttons[0][0].getText().equals(this.buttons[1][1].getText()) && this.buttons[1][1].getText().equals(this.buttons[2][2].getText()) && !this.buttons[1][1].getText().isEmpty()) {
            this.updateScore(this.buttons[0][0].getText());
            this.displayWinner(this.buttons[0][0].getText());
        }

        if (this.buttons[2][0].getText().equals(this.buttons[1][1].getText()) && this.buttons[1][1].getText().equals(this.buttons[0][2].getText()) && !this.buttons[1][1].getText().isEmpty()) {
            this.updateScore(this.buttons[1][1].getText());
            this.displayWinner(this.buttons[1][1].getText());
        }

    }

    private void displayWinner(String winner) {
        Alert alert = new Alert(AlertType.INFORMATION);
        alert.setTitle("And the Winner is ");
        alert.setContentText("Winner is " + winner);
        alert.setHeaderText("");
        alert.showAndWait();
        this.restart();
    }

    private void restart() {
        for(int i = 0; i < 3; ++i) {
            for(int j = 0; j < 3; ++j) {
                this.buttons[j][i].setText("");
            }
        }

    }

    public static void main(String[] args) {
        launch(new String[0]);
    }
}
