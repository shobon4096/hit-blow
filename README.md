# hit-blow

import java.util.*;

public class HitAndBlowkanse {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("hit&blowへようこそ");
        while (true) {
            System.out.print("ゲームを始める方は1\nゲームを終わる方は0\nを入力してください");
            try{
                int game = sc.nextInt();
                if (game == 1) {
                    iti();                                                      //gamestart
                }else if (game == 0){
                    zero();                                                     //gameover
                }else{
                    throw new Exception();
                }
            } catch (Exception e) {
                System.out.println("無効な入力です");                            //{
                sc.nextLine();                                                  //0又は1以外が入力された場合再入力
                continue;
            }                                                                   //}
            break;
        }
    }

    public static void zero() {
        System.out.println("gameover");
        System.exit(0);
    }

    public static void iti() {
        System.out.println("gamestart");
        sanketa();
    }

    public static void sanketa() {
        Random ran = new Random();
        int[] hai = new int[3];
        int i = 0;
        while (true) {
            hai[0] = ran.nextInt(10);                                           //{
            hai[1] = ran.nextInt(10);                                           //3桁の整数をランダムに入力
            hai[2] = ran.nextInt(10);                                           //}
            if (hai[0] == hai[1]) {                                             //{
                continue;
            }else if (hai[0] == hai[2]) {
                continue;                                                       //配列内の数字を重複させない
            }else if (hai[1] == hai[2]) {
                continue;
            }                                                                   //}
            // System.out.print(hai[0]);
            // System.out.print(hai[1]);
            // System.out.println(hai[2]);
            System.out.println("ランダムな3桁の整数が入力されました\n3桁の整数を予想して0~9の値を\"1桁ずつ\"入力してください");
            break;
        }
        startGame(hai);
    }

    public static void startGame(int[] array) {
        Scanner sc = new Scanner(System.in);
        int i = 6;                                                              //{ライフ数}
        
        while (i > 0) {
            int Hit = 0;
            int Blow = 0;
            
            try {                                                               //{
                int yoso = sc.nextInt();
                int yoso1 = sc.nextInt();
                int yoso2 = sc.nextInt();
                if (yoso == array[0]) {
                    Hit += 1;
                }else if (yoso == array[1] || yoso == array[2]) {
                    Blow += 1;
                }try {
                    if (yoso1 == yoso) {
                        throw new Exception();
                    }else if (yoso1 == array[1]) {
                        Hit += 1;
                    }else if (yoso1 == array[0] || yoso1 == array[2]) {         //同じ数字が入力された場合再入力
                        Blow += 1;
                    }
                    if (yoso2 == yoso || yoso2 == yoso1) {
                        throw new Exception();
                    }else if (yoso2 == array[2]) {
                        Hit += 1;
                    }else if (yoso2 == array[0] || yoso2 == array[1]) {
                        Blow += 1;
                    }
                } catch (Exception e) {
                    System.out.println("同じ数字は入力できません\nやり直してください");
                    sc.nextLine();
                    continue;
                }                                                               //}
                System.out.println("Hit:" + Hit + "\nBlow:" + Blow);
                if (yoso == array[0] && yoso1 == array[1] && yoso2 == array[2]) {
                    System.out.println("Congratulation!!!");
                    break;
                }
            } catch (Exception e) {
                System.out.println("error\nやり直して下さい");                  //{
                sc.nextLine();                                                  //0~9以外が入力された場合再入力
                sanketa();                                                      //}
            }
            i--;
            System.out.println("残りライフ" + i);
        }
        if (i == 0) {                                                           //{
            System.out.print("残念ながらゲームは終了しました。\n正解は");
            for (int j = 0; j < array.length; j++) {
                System.out.print(array[j]);                                     //残ライフ0によりgameover
            }
            System.out.println("でした。");
            zero();
        }                                                                       //}
        System.out.println("ゲームはクリアされました");                         //{gameclear}
    }
}
