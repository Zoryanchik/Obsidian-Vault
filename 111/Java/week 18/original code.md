```
```java
import javax.swing.JFrame;
import javax.swing.JPanel;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TilePuzzle implements ActionListener{
    TilePiece[][] tiles = new TilePiece[3][4];
    TilePiece blankTilePiece;

    public static void GUI(){
        JFrame frame = new JFrame("Puzzle!XyiaZle!");
        frame.setSize(475, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
        JPanel panel = new JPanel();
        frame.setContentPane(panel);
        GridLayout layout = new GridLayout(3, 4);
        panel.setLayout(layout);
        int xui =0;
        
        TilePuzzle puzzle = new TilePuzzle();//create puzzle piece soo we can call it

        for(int i = 0; i < 3; i++){
            for (int j = 0; j < 4; j++){
                TilePiece piece;
                if (xui==0){
                    piece = new TilePiece("blank_tile.jpg", j, i);
                    puzzle.blankTilePiece = piece;
                } else{             
              piece = new TilePiece("tile_"+xui+".jpg", j, i);
                }
                piece.addActionListener(puzzle);//we add to piece listener on puzzle
                xui++;
                panel.add(piece);
            }

       }
     
    }
    public void actionPerformed(ActionEvent e)
    {
        TilePiece t = (TilePiece) e.getSource(); // Get an object reference to the tile which has been pressed
        
        if (t.isAdjacentTo(blankTilePiece)){
            t.exchangeImageWith(blankTilePiece);
            blankTilePiece = t;
        }
        // your gameplay code goes here
    }
    
}

``