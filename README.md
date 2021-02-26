interface AttackJudge {
    static final double bloodGrid = 25.0;
    String[] skill_player = {"江南", "缠绵", "止水", "碧影", "蝶舞","A"};
    String[] skill_monster = {"影舞 形", "影舞 影", "影舞 极", "影舞 魂", "影舞 月","影舞 云水雅韵"};
    String[] equip_monster = {"春江月夜", "关山三叹", "镜花水月", "阳春白雪", "昆玉华章"};
    class skill1_player{
        static String name = skill_player[0];
        static int attack = 20;
    }
    class skill2_player{
        static String name = skill_player[1];
        static int attack = 30;
    }
    class skill3_player{
        static String name = skill_player[2];
        static int attack = 50;
    }
    class skill4_player{
        static String name = skill_player[3];
        static int attack = 80;
    }
    class skill5_player{
        static String name = skill_player[4];
        static int attack = 100;
    }
    class skill1_monster{
        static String name = skill_monster[0];
        static int attack = 20;
    }
    class skill2_monster{
        static String name = skill_monster[1];
        static int attack = 30;
    }
    class skill3_monster{
        static String name = skill_monster[2];
        static int attack = 50;
    }
    class skill4_monster{
        static String name = skill_monster[3];
        static int attack = 80;
    }
    class skill5_monster{
        static String name = skill_monster[4];
        static int attack = 100;
    }
    class equip1{
        static String name = "春江月夜";
        static int attack = 20;
        static int define = 10;
    }
    class equip2{
        static String name = "关山三叹";
        static int attack = 30;
        static int define = 15;
    }
    class equip3{
        static String name = "镜花水月";
        static int attack = 30;
        static int define = 40;
    }
    class equip4{
        static String name = "阳春白雪";
        static int attack = 50;
        static int define = 40;
    }
    class equip5{
        static String name = "昆玉华章";
        static int attack = 60;
        static int define = 30;
    }

    void attack(Player p, Monster m);

    void show();
}
public class Monster extends Character implements AttackJudge {

    Monster(String name, int HPMax, int attack, int define, int equipNum) {
        this.name = name;
        this.HPMax = HPMax;
        this.attack = attack;
        this.HP = HPMax;
        this.define = define;
        switch (equipNum) {
            case 0:
                this.equip = equip1.name;
                this.attack += equip1.attack;
                this.define += equip1.define;
                break;
            case 1:
                this.equip = equip2.name;
                this.attack += equip2.attack;
                this.define += equip2.define;
                break;
            case 2:
                this.equip = equip3.name;
                this.attack += equip3.attack;
                this.define += equip3.define;
                break;
            case 3:
                this.equip = equip4.name;
                this.attack += equip4.attack;
                this.define += equip4.define;
                break;
            case 4:
                this.equip = equip5.name;
                this.attack += equip5.attack;
                this.define += equip5.define;
                break;
        }
    }

    @Override
    public void attack(Player p, Monster m) {
        System.out.println("现在是【" + m.getName() + "】的回合：");
        int randNum = (int) (Math.random() * 6);
        int finalAttack = this.attack;
        String attackName = null;
        switch (randNum) {
            case 0:
                finalAttack += skill1_monster.attack;
                attackName = skill1_monster.name;
                break;
            case 1:
                finalAttack += skill2_monster.attack;
                attackName = skill2_monster.name;
                break;
            case 2:
                finalAttack += skill3_monster.attack;
                attackName = skill3_monster.name;
                break;
            case 3:
                finalAttack += skill4_monster.attack;
                attackName = skill4_monster.name;
                break;
            case 4:
                finalAttack += skill5_monster.attack;
                attackName = skill5_monster.name;
                break;
            case 5:
                attackName = "影舞 云水雅韵";
                break;
        }
        finalAttack -= p.getDefine();
        if (finalAttack > 0) {
            p.setHP(p.getHP() - finalAttack);
            System.out.println("【" + m.getName() + "】对【" + p.getName() + "】使用了@@" + attackName + "@@,造成了" + finalAttack + "点伤害");
        } else System.out.println(m.getName() + "免疫");
        System.out.println(m.getName() + "的回合结束。");
    }


    @Override
    public void show() {
        int j;
        System.out.print("【" + getName() + "】的血量为：");
        for (j = 0; j < getHP() / bloodGrid; j++) System.out.print("■");
        for (j = 0; j < (getHPMax() - getHP()) / bloodGrid; j++) System.out.print("□");
        System.out.println();
    }
}
import java.util.Scanner;

public class Player extends Character implements AttackJudge {
    Player(String name, int HPMax, int attack, int define) {
        this.name = name;
        this.HPMax = HPMax;
        this.HP = HPMax;
        this.attack = attack;
        this.define = define;
    }

    @Override
    public void attack(Player p, Monster m) {
        System.out.println("现在是【" + p.getName() + "】的回合：");
        int randNum = (int) (Math.random() * 6);
        int finalAttack = this.attack;
        String attackName = null;
        switch (randNum) {
            case 0 :
                finalAttack += skill1_player.attack;
                attackName = skill1_player.name;
                break;
            case 1 :
                finalAttack += skill2_player.attack;
                attackName = skill2_player.name;
                break;
            case 2 :
                finalAttack += skill3_player.attack;
                attackName = skill3_player.name;
                break;
            case 3 :
                finalAttack += skill4_player.attack;
                attackName = skill4_player.name;
                break;
            case 4 :
                finalAttack += skill5_player.attack;
                attackName = skill5_player.name;
                break;
            case 5 :attackName = "A";
                break;
        }
        finalAttack -= m.getDefine();
        if (finalAttack < 0) finalAttack = 0;
        m.setHP(m.getHP() - finalAttack);
        System.out.println("【" + p.getName() + "】对【" + m.getName() + "】使用了@@" + attackName + "@@,造成了" + finalAttack + "点伤害");
        System.out.println("作战结束");
    }
    @Override
    public void show() {
        int j;
        System.out.print("【" + getName() + "】" + "的血量为：");
        for (j = 0; j < getHP() / bloodGrid; j++) System.out.print("■");
        for (j = 0; j < (getHPMax() - getHP()) / bloodGrid; j++) System.out.print("□");
        System.out.println();
    }
}

# test2
作业2
