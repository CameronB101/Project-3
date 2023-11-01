# Project-3 
#include <iostream>
#include <iomanip>
using namespace std;

const int ROW = 10; // constant to hold the number of rows
const int COL = 30; // constant to hold the number of columns

// function to initialize the seating chart
void initializeSeats(char seats[ROW][COL])
{
    for (int i = 0; i < ROW; i++)
        for (int j = 0; j < COL; j++)
            seats[i][j] = '#';
}

// function to print the seating chart
void displaySeatingPlan(char seats[ROW][COL])
{
    cout << "Seats:    ";
    for (int j = 0; j < COL; j++)
    {
        cout << j << "  ";
    }
    cout << "\n\n";

    for (int i = 0; i < ROW; i++)
    {
        cout << "Row " << left << setw(2) << i << ":   ";
        for (int j = 0; j < COL; j++)
        {
            cout << seats[i][j] << "  ";
            if (j >= 9)
                cout << " ";
        }
        cout << "\n";
    }
}

/// function to sell a particular ticket
void sellTicket(char seats[ROW][COL], double prices[ROW], int &totalTickets, double &totalRevenue)
{
    int row, col;
    char ch = 'y';
    while (ch == 'y')
    {
        cout << "Seat desired (row, column): ";
        cin >> row >> col;

        if ((row < 0 || row > 14) || (col < 0 || col > 19))
            cout << "Out of range\n";
        else if (seats[row][col] == '*')
            cout << "Seat already taken\n";
        else
        {
            seats[row][col] = '*';
            cout << "Charge: $" << prices[row] << "\n";
            totalTickets++;
            totalRevenue += prices[row];
        }
        cout << "Buy another ticket (y = yes)?: ";
        cin >> ch;
    }
}

// main function
int main()
{
    char seats[ROW][COL];
    double prices[ROW] = {40.00, 40.00, 35.00, 35.00, 35.00, 30.00, 30.00, 25.00, 25.00, 25.00};
    int totalTickets = 0;
    double totalRevenue = 0;

    cout.setf(ios::fixed);
    cout.precision(2);

    initializeSeats(seats);
    cout << "\n--------------------\n";
    cout << "CURRENT SEATING CHART:\n";
    cout << "--------------------\n";
    displaySeatingPlan(seats);

    int option;

    while (true)
    {
        cout << "\nSelect an option:\n";
        cout << "1. Buy Ticket\n";
        cout << "2. Display seating and sales\n";
        cout << "0. Quit\n\n";
        cout << "Selection: ";
        cin >> option;

        if (option == 0)
        {
            cout << "\nThank You!\n";
            break;
        }

        switch (option)
        {
        case 1:
            sellTicket(seats, prices, totalTickets, totalRevenue);
            break;
        case 2:
            cout << "\n--------------------\n";
            cout << "UPDATED SEATING CHART AND SALES INFO:\n";
            cout << "--------------------\n";
            displaySeatingPlan(seats);
            cout << "TOTAL TICKETS SOLD: " << totalTickets << "\n";
            cout << "TOTAL REVENUE: $" << totalRevenue << "\n\n";
            break;
        default:
            cout << "\nInvalid Selection!\n";
            break;
        }
    }

    return 0;
}
