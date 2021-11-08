#include <time.h>
#include <iostream>
#include <string>
#include <iomanip>
#include <cstdlib>

using namespace std;

typedef unsigned int obj;
enum rodykles { UP, DOWN, LEFT, RIGHT };

class plytele
{
public:
    plytele() : reiksme( 0 ), uzimta( false ) {}
    obj reiksme;
    bool uzimta;
};

class zaidimas
{
public:
    zaidimas() : pabaiga( false ), laimejimas( false ), pajudejimas( true ) {}
    void ciklas()
    {
	ideti2();
	while( true )
	{
	    if( pajudejimas != 0 ) ideti2();
	    PiestiLentele();
	    if( pabaiga != 0 ) break;
	    direction();
	}
	string s = "Pabaiga!";
	if( laimejimas ) s = "Laimejai!";
	cout << s << endl << endl;
    }
private:
    plytele matrica[4][4];
    bool laimejimas, pabaiga, pajudejimas;
    void PiestiLentele()
    {
	system( "cls" );
	for( int y = 0; y < 4; y++ )
	{
	    cout << "-----------------------------" << endl << "| ";
	    for( int x = 0; x < 4; x++ )
	    {
		if( matrica[x][y].reiksme == 0 ) cout << setw( 4 ) << " ";
		else cout << setw( 4 ) << matrica[x][y].reiksme;
		cout << " | ";
	    }
	    cout << endl;
	}
	cout << "-----------------------------" << endl << endl;
    }
    void direction()
    {
	pajudejimas = false; char c;
	cout << "(w)aukstyn (s)zemyn (a)kairen (d)desinen "; cin >> c;
	switch( c )
	{
	    case 'w': move( UP );break;
	    case 'a': move( LEFT ); break;
	    case 's': move( DOWN ); break;
	    case 'd': move( RIGHT );
	}
	for( int y = 0; y < 4; y++ )
	    for( int x = 0; x < 4; x++ )
		matrica[x][y].uzimta = false;
    }
    void ideti2()
    {
	for( int y = 0; y < 4; y++ )
	    for( int x = 0; x < 4; x++ )
		if( matrica[x][y].reiksme == 0 )
		{
		    obj a, b;
		    do
		    { a = rand() % 4; b = rand() % 4; }
		    while( matrica[a][b].reiksme != 0 );

            matrica[a][b].reiksme = 2;
		    if( Zingsniai() ) return;
		}
	pabaiga = true;
    }
    bool Zingsniai()
    {
	for( int y = 0; y < 4; y++ )
	    for( int x = 0; x < 4; x++ )
		if( matrica[x][y].reiksme == 0) return true;

	for( int y = 0; y < 4; y++ )
	    for( int x = 0; x < 4; x++ )
	    {
		if( testas( x + 1, y, matrica[x][y].reiksme ) ) return true;
		if( testas( x - 1, y, matrica[x][y].reiksme ) ) return true;
		if( testas( x, y + 1, matrica[x][y].reiksme ) ) return true;
		if( testas( x, y - 1, matrica[x][y].reiksme ) ) return true;
	    }
	return false;
    }
    bool testas( int x, int y, obj v )
    {
	if( x < 0 || x > 3 || y < 0 || y > 3 ) return false;
	return matrica[x][y].reiksme == v;
    }
    void updown( int x, int y, int d )
    {
	if( matrica[x][y+d].reiksme != 0 && matrica[x][y + d].reiksme == matrica[x][y].reiksme && matrica[x][y].uzimta == 0 && matrica[x][y + d].uzimta == 0 )
	{
	    matrica[x][y].reiksme = 0;
	    matrica[x][y + d].reiksme *= 2;

	    matrica[x][y + d].uzimta = true;
	    pajudejimas = true;
	}
	else if( matrica[x][y + d].reiksme == 0 && matrica[x][y].reiksme != 0 )
	{
	    matrica[x][y + d].reiksme = matrica[x][y].reiksme;
	    matrica[x][y].reiksme = 0;
	    pajudejimas = true;
	}
	if( d > 0 ) { if( y + d < 3 ) updown( x, y + d,  1 ); }
	else        { if( y + d > 0 ) updown( x, y + d, -1 ); }
    }
    void leftright( int x, int y, int d )
    {
	if( matrica[x+d][y].reiksme != 0 && matrica[x + d][y].reiksme == matrica[x][y].reiksme && matrica[x][y].uzimta == 0 && matrica[x + d][y].uzimta == 0 )
	{
	    matrica[x][y].reiksme = 0;
	    matrica[x + d][y].reiksme *= 2;

	    matrica[x + d][y].uzimta = true;
	    pajudejimas = true;
	}
	else if( matrica[x + d][y].reiksme == 0 && matrica[x][y].reiksme != 0 )
	{
	    matrica[x + d][y].reiksme = matrica[x][y].reiksme;
	    matrica[x][y].reiksme = 0;
	    pajudejimas = true;
	}
	if( d > 0 ) { if( x + d < 3 ) leftright( x + d, y,  1 ); }
	else        { if( x + d > 0 ) leftright( x + d, y, -1 ); }
    }
    void move( rodykles d )
    {
	switch( d )
	{
	    case UP:
	    	for( int x = 0; x < 4; x++ )
		{
		    int y = 1;
		    while( y < 4 )
		    { if( matrica[x][y].reiksme != 0 ) updown( x, y, -1 ); y++;}
		}
		break;
	    case DOWN:
		for( int x = 0; x < 4; x++ )
		{
		    int y = 2;
		    while( y >= 0 )
		    { if( matrica[x][y].reiksme != 0 ) updown( x, y, 1 ); y--;}
		}
		break;
	    case LEFT:
		for( int y = 0; y < 4; y++ )
		{
		    int x = 1;
		    while( x < 4 )
		    { if( matrica[x][y].reiksme != 0 ) leftright( x, y, -1 ); x++;}
		}
		break;
	    case RIGHT:
		for( int y = 0; y < 4; y++ )
		{
		    int x = 2;
		    while( x >= 0 )
		    { if( matrica[x][y].reiksme != 0 ) leftright( x, y, 1 ); x--;}
		}
	}
    }

};

int main( int argc, char* argv[] )
{
    srand( static_cast<obj>( time( NULL ) ) );
    zaidimas z;
    z.ciklas();
    return system( "pause" );
}
