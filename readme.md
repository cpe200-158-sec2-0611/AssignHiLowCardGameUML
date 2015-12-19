## Hi Low Card Game UML Design
##### To-do: fork to your own organization (cpe200-158-sec1-0XXX), upload your UML diagram as image, edit readme file to attach your UML diagram to readme file, change your student id, and send pull request to main repository
###### Note that you can edit readme file online, or use anything as you can.
###### Due date: 10/30/2015 17:00:00 PM

 Student ID: 570610611
 
 ![570610611](http://www.mx7.com/i/1f1/mrVE1H.png)
 แก้นะครับ ![570610611](http://www.mx7.com/i/c4c/9zDLbe.png)
 พอดี push ไม่ได้สักที แก้ตรงนี้เลยนะครับ
 
_________________________________________________________________________ 

 ไฟล์ deck.cs
 
 using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace HighLow_TheEndOfCardgame
{
    class deck
    {
        private Stack<card> card_deck;


        public deck(int num = 0)
        {
            card_deck = new Stack<card>(num);

            if(num==52) //maindeck
            {
                //(♥), diamonds(♦) and clubs (♣)
                card_deck.Push(new card(2, "2♠"));
                card_deck.Push(new card(2, "2♦"));
                card_deck.Push(new card(2, "2♣"));
                card_deck.Push(new card(2, "2♥"));

                card_deck.Push(new card(3, "3♠"));
                card_deck.Push(new card(3, "3♦"));
                card_deck.Push(new card(3, "3♣"));
                card_deck.Push(new card(3, "3♥"));

                card_deck.Push(new card(4, "4♠"));
                card_deck.Push(new card(4, "4♦"));
                card_deck.Push(new card(4, "4♣"));
                card_deck.Push(new card(4, "4♥"));

                card_deck.Push(new card(5, "5♠"));
                card_deck.Push(new card(5, "5♦"));
                card_deck.Push(new card(5, "5♣"));
                card_deck.Push(new card(5, "5♥"));

                card_deck.Push(new card(6, "6♠"));
                card_deck.Push(new card(6, "6♦"));
                card_deck.Push(new card(6, "6♣"));
                card_deck.Push(new card(6, "6♥"));

                card_deck.Push(new card(7, "7♠"));
                card_deck.Push(new card(7, "7♦"));
                card_deck.Push(new card(7, "7♣"));
                card_deck.Push(new card(7, "7♥"));

                card_deck.Push(new card(8, "8♠"));
                card_deck.Push(new card(8, "8♦"));
                card_deck.Push(new card(8, "8♣"));
                card_deck.Push(new card(8, "8♥"));

                card_deck.Push(new card(9, "9♠"));
                card_deck.Push(new card(9, "9♦"));
                card_deck.Push(new card(9, "9♣"));
                card_deck.Push(new card(9, "9♥"));

                card_deck.Push(new card(10, "10♠"));
                card_deck.Push(new card(10, "10♦"));
                card_deck.Push(new card(10, "10♣"));
                card_deck.Push(new card(10, "10♥"));

                card_deck.Push(new card(11, "Jack♠"));
                card_deck.Push(new card(11, "Jack♦"));
                card_deck.Push(new card(11, "Jack♣"));
                card_deck.Push(new card(11, "Jack♥"));

                card_deck.Push(new card(12, "Queen♠"));
                card_deck.Push(new card(12, "Queen♦"));
                card_deck.Push(new card(12, "Queen♣"));
                card_deck.Push(new card(12, "Queen♥"));

                card_deck.Push(new card(13, "King♠"));
                card_deck.Push(new card(13, "King♦"));
                card_deck.Push(new card(13, "King♣"));
                card_deck.Push(new card(13, "King♥"));

                card_deck.Push(new card(14, "Ace♠"));
                card_deck.Push(new card(14, "Ace♦"));
                card_deck.Push(new card(14, "Ace♣"));
                card_deck.Push(new card(14, "Ace♥"));
            }
        }

        public card drawcard()
        {
            return card_deck.Pop();
        }

        public void pushcard(card c)
        {
            card_deck.Push(c);
        }
        public int getnumcard()
        {
            return card_deck.Count;
        }

        public void shuffle()
        {
            Random r = new Random();
            for (int n = card_deck.Count - 1; n > 0; --n)
            {
                int k = r.Next(n + 1);
                card temp = card_deck.ElementAt(k);

                card_deck.ElementAt(n).switchcardval(card_deck.ElementAt(k));
                card_deck.ElementAt(k).switchcardval(temp);
            }
        }
    }
}

_________________________________________________________________________ 

card.cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace HighLow_TheEndOfCardgame
{
    class card
    {

        private int val;
        private string name;

        public card(int val = 14 ,string name = "Ace♠")
        {

            this.val = val;
            this.name = name;
        }

        public int getval()
        { return val; }

        public string getname()
        { return name; }

        public void switchcardval(card c)
        {
            name = c.getname();
            val = c.getval();
        }

    }
}

_________________________________________________________________________ 

ที่เหลือเป็น Form1.cs

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace HighLow_TheEndOfCardgame
{
    public partial class Form1 : Form
    {

        deck p1_deck = new deck(0);
        deck p2_deck = new deck(0);
        deck main_deck = new deck(52);
        bool checkend = false;
        public Form1()
        {
            InitializeComponent();


            main_deck.shuffle();

            for (int i = 0; i < 26; i++)
            {
                
                p1_deck.pushcard(main_deck.drawcard());
                p2_deck.pushcard(main_deck.drawcard());
            }

            P1_num.Text = p1_deck.getnumcard()+" card";
            P2_num.Text = p2_deck.getnumcard() + " card";
        }

        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            if(!checkend)
            {
            card p1_drawcard,p2_drawcard;

            p1_drawcard = p1_deck.drawcard();
            p2_drawcard = p2_deck.drawcard();

            P1_txt.Text = p1_drawcard.getname();
            P2_txt.Text = p2_drawcard.getname();

            if (p1_drawcard.getval() != p2_drawcard.getval())
            {
                p1_drawagain.Text = "";
                p2_drawagain.Text = "";

                if (p1_drawcard.getval() > p2_drawcard.getval())
                {
                    p1_deck.pushcard(p1_drawcard);
                    p1_deck.pushcard(p2_drawcard);
                    maintxt.Text = "P1 Win this Match";

                }
                else
                {
                    p2_deck.pushcard(p1_drawcard);
                    p2_deck.pushcard(p2_drawcard);
                    maintxt.Text = "P2 Win this Match";

                }
            }
            else
            {
                int sameval = p1_drawcard.getval();
                if(sameval == 14)
                { sameval = 1; }

                p1_drawagain.Text = "P1 Draw Again";
                p2_drawagain.Text = "P2 Draw Again";

                Stack<card> p1_card_again = new Stack<card>(0);
                Stack<card> p2_card_again = new Stack<card>(0);

                if(p1_deck.getnumcard()<sameval)
                {
                    for (int i = 0; i < p1_deck.getnumcard(); i++)
                    {
                        p1_card_again.Push(p1_deck.drawcard());
                        p1_drawagain.Text += " "+p1_card_again.ElementAt(0).getname();
                    }
                }
                else
                {
                    for (int i = 0; i < sameval; i++)
                    {
                        p1_card_again.Push(p1_deck.drawcard());
                        p1_drawagain.Text += " " + p1_card_again.ElementAt(0).getname();
                    }
                }

                if (p2_deck.getnumcard() < sameval)
                {
                    for (int i = 0; i < p2_deck.getnumcard(); i++)
                    {
                        p2_card_again.Push(p2_deck.drawcard());
                        p2_drawagain.Text += " " + p2_card_again.ElementAt(0).getname();
                    }
                }
                else
                {
                    for (int i = 0; i < sameval; i++)
                    {
                        p2_card_again.Push(p2_deck.drawcard());
                        p2_drawagain.Text += " " + p2_card_again.ElementAt(0).getname();
                    }
                }


                if (p1_card_again.ElementAt(p1_card_again.Count-1).getval() > p2_card_again.ElementAt(p2_card_again.Count - 1).getval())
                {
                    int p1_again_size = p1_card_again.Count;
                    int p2_again_size = p2_card_again.Count;

                    for (int i = 0; i < p1_again_size; i++)
                    {
                        p1_deck.pushcard(p1_card_again.Pop());
                    }

                    for (int i = 0; i < p2_again_size; i++)
                    {
                        p1_deck.pushcard(p2_card_again.Pop());
                    }

                    p1_deck.pushcard(p1_drawcard);
                    p1_deck.pushcard(p2_drawcard);
                    maintxt.Text = "P1 Win this Match";

                }
                else if (p1_card_again.ElementAt(p1_card_again.Count - 1).getval() < p2_card_again.ElementAt(p2_card_again.Count - 1).getval())
                {
                    int p1_again_size = p1_card_again.Count;
                    int p2_again_size = p2_card_again.Count;

                    for (int i = 0; i < p1_again_size; i++)
                    {
                        p2_deck.pushcard(p1_card_again.Pop());
                    }

                    for (int i = 0; i < p2_again_size; i++)
                    {
                        p2_deck.pushcard(p2_card_again.Pop());
                    }


                    p2_deck.pushcard(p1_drawcard);
                    p2_deck.pushcard(p2_drawcard);
                    maintxt.Text = "P2 Win this Match";

                }
                else
                {

                    int p1_again_size = p1_card_again.Count;
                    int p2_again_size = p2_card_again.Count;

                    for (int i = 0; i < p1_again_size; i++)
                    {
                        p1_deck.pushcard(p1_card_again.Pop());
                    }

                    for (int i = 0; i < p2_again_size; i++)
                    {
                        p2_deck.pushcard(p2_card_again.Pop());
                    }


                    p1_deck.pushcard(p1_drawcard);
                    p2_deck.pushcard(p2_drawcard);
                }

            }


            P1_num.Text = p1_deck.getnumcard() + " card";
            P2_num.Text = p2_deck.getnumcard() + " card";

                if(p1_deck.getnumcard() == 0||p2_deck.getnumcard()==0)
                { checkend = true; }
            }
        }
    }
}

แก้ไขใหม่นะครับ
ไฟล์เต็มที่ run ได้ อยู่ใน googledrive นะครับ ขอบคุณครับ 
https://drive.google.com/open?id=0B95TDpZk_D8Ib2xzVl80RVVtaWM
