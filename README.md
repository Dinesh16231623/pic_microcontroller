# pic_microcontroller
//Display a string in LCD Display in PICF16887 Microcontroller..

// CONFIG1
#pragma config FOSC = INTRC_NOCLKOUT// Oscillator Selection bits (INTOSCIO oscillator: I/O function on RA6/OSC2/CLKOUT pin, I/O function on RA7/OSC1/CLKIN)
#pragma config WDTE = OFF       // Watchdog Timer Enable bit (WDT disabled and can be enabled by SWDTEN bit of the WDTCON register)
#pragma config PWRTE = ON       // Power-up Timer Enable bit (PWRT enabled)
#pragma config MCLRE = ON       // RE3/MCLR pin function select bit (RE3/MCLR pin function is MCLR)
#pragma config CP = OFF         // Code Protection bit (Program memory code protection is disabled)
#pragma config CPD = OFF        // Data Code Protection bit (Data memory code protection is disabled)
#pragma config BOREN = OFF      // Brown Out Reset Selection bits (BOR disabled)
#pragma config IESO = ON        // Internal External Switchover bit (Internal/External Switchover mode is enabled)
#pragma config FCMEN = ON       // Fail-Safe Clock Monitor Enabled bit (Fail-Safe Clock Monitor is enabled)
#pragma config LVP = OFF        // Low Voltage Programming Enable bit (RB3 pin has digital I/O, HV on MCLR must be used for programming)

// CONFIG2
#pragma config BOR4V = BOR40V   // Brown-out Reset Selection bit (Brown-out Reset set to 4.0V)
#pragma config WRT = OFF        // Flash Program Memory Self Write Enable bits (Write protection off)

// #pragma config statements should precede project file includes.
// Use project enums instead of #define for ON and OFF.

#include <xc.h>
#define LCD PORTD
#define RW RC6
#define RS RC5
#define EN RC7
void delay(int a);
void type(char a);
void on(char a);
void address(char a);
void display(char a);
void string(char *ptr);



int main()
{
 PORTD=0X00;TRISD=0X00;
 PORTC=0X00;TRISC=0X00;
 ANSEL=0X00;ANSELH=0X00;
 
    type(0X38);
    on(0X0E);
    address(0X80);
    string("PRINTING STRING");
    while(1);
    
}

void delay(int a)
{
    while(a--);
}
void pulse()
{
    EN=1;
    delay(1000);
    EN=0;
    delay(1000);
}
void type(char a)
{
    RS=0;RW=0;
    LCD=a;
    pulse();
}
void on(char a)
{
    RS=0;RW=0;
    LCD=a;
    pulse();
}
void address(char a)
{
    RS=0;RW=0;
    LCD=a;
    pulse();
}
void display(char a)
{   
    RS=1;
    LCD=a;
    pulse();
    }  

void string(char *ptr)
{
    while(*ptr)
    display(*ptr++);
}

