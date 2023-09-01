# recognition of differnt part 
## Tile
 >The only method of this class you’ll need to use is `.value()` which returns the value of the given tile. For example if `Tile t` corresponds to a tile with the value 8, then `t.value()` will return `8`.
 
 ## Side 
 *Side is a enum type in java which represent the set of directions such as 'north' ,'south' etc.*
 We will not use this as the Josh said

## Board

This class represents the board of tiles itself. It has three methods that you’ll use: `setViewingPerspective`, `tile`, `move`. Optionally, for experimentation, you can use `getRandomNonNullTile`.

**You will only edit the `Model.java` file in this assignment.** Gradescope will only take your `Model.java` file and use the skeleton versions of the other files, so if you make an edit to `Tile.java` for example, it will not be recognized by Gradescope.

# My assignment
Your job for this project is to modify and complete the `Model` class, specifically the `emptySpaceExists`, `maxTileExists`, `atLeastOneMoveExists` and `tilt` methods.

## emptySpaceExists
 you’ll want to use the `tile(int col, int row)` and `size()` methods of the `Board` class
 Solution
```java
public static boolean emptySpaceExists(Board b) {
        // TODO: Fill in this function.

        for(int i=0;i<b.size();i++)
        {
            for(int j=0;j<b.size();j++)
            {
                if(b.tile(i,j)==null)
                {
                    return  true;
                }
            }
        }//iterate the Board b tile
        return false;
    }
```
通过遍历的方式实现判断 emptySpace

## public static boolean maxTileExists(Board b)
check if there are MAX_PIECE(2048) in the Board  , if there are return true;
it resembles the ` emptySpaceExists` Method 
use the iteration

## public static boolean atLeastOneMoveExists(Board b)

This method is more challenging. It should return true if there are any valid moves. By a “valid move”, we mean that if there is a button (UP, DOWN, LEFT, or RIGHT) that a user can press while playing 2048 that causes at least one tile to move, then such a keypress is considered a valid move.

先判断是否有空位置
然后根据临近的tile 判断`adjacentSame`的bool值
在 `adjacentValid`fucntion中 我只进行下和右的判断来简化边界条件（bound exception）
```java
 public static boolean adjacentValid(Board b, int i ,int j)
    {
        if (i!=b.size()-1 && j!= b.size()-1) //the 1st situation which is the normal
        {
            if(b.tile(i,j).value()==b.tile(i+1,j).value()|| b.tile(i,j).value()==b.tile(i,j+1).value()) {
                return true; //in the West or South direction have the same value
            }
        }
        else if(i!=b.size()-1 && j== b.size()-1)
        {
            if(b.tile(i,j).value()==b.tile(i+1,j).value())
                return true;
        } else if ( i== b.size()-1 && j!=b.size()-1) {
           if (b.tile(i,j).value()==b.tile(i,j+1).value())
               return true;
        }
        return false;
    }
```

# Main Task (may be challenging to complete the `Tilt` function)

主要思路是将board以单独的column遍历 从 board的max row 往上查找 

代码不难但是比较坑的是  当board的side 改变之后
```java
t.col();
t.row();
//都不是我们改变方向后board 的 coordinates 而是 NORTH向的
//因此我用 `desrow` int 来表示

```

而 Topchange 和 SecChange 则是为了解决 （2，2，2，2） 和 （4，2，2） 这两种情况
*感谢Junit Testing*


## Small bug
❗ 在 GUISource 中 key会导致我们游戏开始 按键无法对游戏产生影响 将箭头改成 wasd
![[image/image/Project 0   game2048-1693575670973.png]]😍[solution reference]([关于CS61b sp21中proj0的问题_cs61b 2048_God_onload的博客-CSDN博客](https://blog.csdn.net/God_onload/article/details/126210507))

# Grade 
FUll MARKs
![[image/image/Project 0   game2048-1693575782486.png]]