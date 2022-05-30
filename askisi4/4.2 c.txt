#include <avr/io.h>

char A,B,C,D,F0,F1;

int main(void) {
	DDRA = 0xFF; //setting A as output
	DDRB = 0x00; //setting B as input
	F0 = F1 = 0x00; //setting output to zero (turned off leds)
	
    while (1) {
		A = PINB&0x01; //getting PB0
		B = (PINB&0x02)>>1; //getting PB1
		C = (PINB&0x04)>>2; //getting PB2
		D = (PINB&0x08)>>3; //getting PB3
		
		F0 = (A&B&C)|(~B&~C&~D); //binary operation
		F1 = ((A|B|C)&D)<<1;	//binary operation
		
		PORTA = ((F0&0x01)|(F1&0x02)); //outputing the combination of F0 and F1 to port A
		
    }
}

