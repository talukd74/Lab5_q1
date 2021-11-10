# Lab5_q1
#include <msp430.h> 
#define Red_LED BIT6
#define Green_LED BIT0
//#define Toggle_LEDs (P1OUT ^= RedLED|GreenLED)
#define Button BIT3



void main(void)
{
    BCSCTL2 |= DIVS_3;
    WDTCTL = WDT_MDLY_32;
    IE1 |= WDTIE;
    P1DIR = Red_LED|Green_LED;
    P1OUT = Red_LED;
    P1IFG =0x00;
    _enable_interrupts();
    LPM1;

    while(1);
}


#pragma vector = WDT_VECTOR
__interrupt void WDT(void)
    {
    P1OUT ^= Red_LED|Green_LED;
    P1IFG =0x00;
        }
