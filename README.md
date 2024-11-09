# Casino-rush
#include <iostream>
#include <ctime>
#include <fstream>
#include <vector>
#include <algorithm>
#include <ctime>
#include <chrono>
#include <thread>
#include "GetRandomNum.h"
#include "Rules.h"
using namespace std;

void saveBudget(int budget) {
    ofstream out("D:\\777.txt");
    if (!out) {
        cout << "Error saving the budget to the file!" << endl;
        return;
    }
    out << budget;
    out.close();
}

int loadBudget() {
    ifstream in("D:\\777.txt");
    int budget = 1000;
    if (in) {
        in >> budget;
    }
    in.close();
    return budget;
}

void slots(int& budget) {
    int bet;
    cout << "\nSlots\n" << endl;

    displayRules(1);
    cout << endl;

    vector<string> symbols = { "CH", "LE", "BE", "ST", "7", "DI" };

    while (budget > 0) {
        cout << "Your budget: " << budget << endl;
        cout << "Bet: 5 - 10 - 20 - 50: ";
        cin >> bet;

        if (bet == 5 || bet == 10 || bet == 20 || bet == 50) {
            if (bet <= budget) {
                budget -= bet;
                cout << endl;
                cout << "Rolling...\n";
                this_thread::sleep_for(chrono::milliseconds(1000));
                int num1 = rand() % symbols.size();
                int num2 = rand() % symbols.size();
                int num3 = rand() % symbols.size();

                cout << endl;
                cout << "Result: " << symbols[num1] << "\t" << symbols[num2] << "\t" << symbols[num3] << endl;

                bool win = false;
                if (num1 == num2 || num2 == num3 || num1 == num3) {
                    cout << "\033[1;32m" << "WIN! -- 5x" << "\033[0m" << endl;
                    budget += bet * 5;
                    win = true;
                }

                if (num1 == num2 && num2 == num3) {
                    cout << "\033[1;32m" << "BIG WIN! -- 20x" << "\033[0m" << endl;
                    budget += bet * 20;
                    win = true;
                }

                if (num1 == 4 && num2 == 4 && num3 == 4) {
                    cout << "\033[1;32m" << "MEGA BIG WIN! -- 100x" << "\033[0m" << endl;
                    budget += bet * 100;
                    win = true;
                }
                if (!win) {
                    cout << "\033[1;31m" << "You lost this round." << "\033[0m" << endl;
                }

                saveBudget(budget);
            }
            else {
                cout << "You don't have enough money for this bet.\n";
            }
        }
        else {
            cout << "Invalid bet, enter 5 - 10 - 20 - 50.\n";
        }

        if (budget == 0) {
            cout << "Your budget is over! Game is over.\n";
            break;
        }
    }
}


void cube(int& budget) {
    int num;
    int bet;
    cout << "\nCube\n" << endl;

    displayRules(2);
    cout << endl;

    while (budget > 0) {
        cout << "Your budget: " << budget << endl;
        cout << "Bet: 5 - 10 - 20 - 50 - 100: ";
        cin >> bet;

        if (bet == 5 || bet == 10 || bet == 20 || bet == 50 || bet == 100) {
            if (bet <= budget) {
                budget -= bet;

                cout << endl;
                cout << "Rolling...\n";
                this_thread::sleep_for(chrono::milliseconds(1000));

                int num1 = rand() % 6 + 1;

                cout << "1 - even number \t2 - odd number" << endl;
                cout << "Pick a choice (1 or 2): ";
                cin >> num;
                cout << endl;

                cout << "Result: " << num1 << endl;

                bool isEven = (num1 % 2 == 0);

                if (num1 == 6) {
                    cout << "\033[1;32m" << "MEGA BIG WIN! -- 20x" << "\033[0m" << endl;
                    budget += bet * 20;
                }
                else if (num1 == 3) {
                    cout << "\033[1;32m" << "BIG WIN! -- 5x" << "\033[0m" << endl;
                    budget += bet * 5;
                }
                else {
                    if ((num == 1 && isEven) || (num == 2 && !isEven)) {
                        cout << "\033[1;32m" << "WIN! -- 2x" << "\033[0m" << endl;
                        budget += bet * 2;
                    }
                    else {
                        cout << "\033[1;31m" << "You lost this round." << "\033[0m" << endl;
                    }
                }
                saveBudget(budget);
            }
            else {
                cout << "You don't have enough money for this bet.\n";
            }
        }
        else {
            cout << "Invalid bet, enter 5 - 10 - 20 - 50 - 100.\n";
        }

        if (budget == 0) {
            cout << "Your budget is over! Game is over.\n";
            break;
        }
    }
}

void plinko(int& budget) {
    int bet;
    cout << "\nPlinko\n" << endl;

    displayRules(3);
    cout << endl;

    while (budget > 0) {
        cout << "Your budget: " << budget << endl;
        cout << "Bet: 5 - 10 - 20 - 50 - 100: ";
        cin >> bet;

        if (bet == 5 || bet == 10 || bet == 20 || bet == 50 || bet == 100) {
            if (bet <= budget) {
                budget -= bet;

                int result = getrandomnum();
                if (result == 1) {
                    cout << "\033[1;32m" << "WIN! -- 0.2x" << "\033[0m" << endl;
                    budget += bet * 0.2;
                }
                else if (result == 2) {
                    cout << "\033[1;32m" << "WIN! -- 0.5x" << "\033[0m" << endl;
                    budget += bet * 0.5;
                }
                else if (result == 3) {
                    cout << "\033[1;32m" << "WIN! -- 2x" << "\033[0m" << endl;
                    budget += bet * 2;
                }
                else if (result == 4) {
                    cout << "\033[1;32m" << "WIN! -- 5x" << "\033[0m" << endl;
                    budget += bet * 5;
                }
                else if (result == 5) {
                    cout << "\033[1;32m" << "WIN! -- 10x" << "\033[0m" << endl;
                    budget += bet * 10;
                }
                else if (result == 6) {
                    cout << "\033[1;32m" << "WIN! -- 100x" << "\033[0m" << endl;
                    budget += bet * 100;
                }
                saveBudget(budget);
            }
            else {
                cout << "\033[1;31m" << "Insufficient budget!" << "\033[0m" << endl;
            }
        }
        else {
            cout << "\033[1;31m" << "Invalid bet amount!" << "\033[0m" << endl;
        }
    }

    cout << "Game over! You have no more money left.\n";
}

struct card {
    string suit;
    string rank;
    int value;
};

vector<card> createDeck() {
    vector<card>deck;
    string ranks[] = { "6", "7", "8", "9", "10", "Jack", "Queen", "King", "Ace" };
    string suits[] = { "Hearts", "Diamonds", "Clubs", "Spades" };
    int values[] = { 6, 7, 8, 9, 10, 10, 10, 10, 11 };
    for (const auto& suit : suits) {
        for (int i = 0; i < 9; ++i) {
            deck.push_back(card{ suit, ranks[i], values[i] });
        }
    }
    return deck;
}

int calculateHandValue(const vector<card>& hand) {
    int total = 0;
    int aceCount = 0;
    for (const auto& c : hand) {
        total += c.value;
        if (c.rank == "Ace") ++aceCount;
    }
    while (total > 21 && aceCount > 0) {
        total -= 10;
        --aceCount;
    }
    return total;
}

void shuffleDeck(vector<card>& deck) {
    random_device rd;
    mt19937 g(rd());
    shuffle(deck.begin(), deck.end(), g);
}

void blackjack(int& budget) {
    cout << "Welcome to Blackjack!" << endl;

    displayRules(4);
    cout << endl;

    vector<card> deck = createDeck();
    shuffleDeck(deck);

    int bet;
    cout << "Your budget: " << budget << endl;
    cout << "Enter your bet (100): ";
    cin >> bet;

    if (bet > budget) {
        cout << "You don't have enough budget for this bet!" << endl;
        return;
    }

    budget -= bet;

    vector<card> playerHand, dealerHand;


    playerHand.push_back(deck.back()); deck.pop_back();
    dealerHand.push_back(deck.back()); deck.pop_back();
    playerHand.push_back(deck.back()); deck.pop_back();
    dealerHand.push_back(deck.back()); deck.pop_back();

    cout << "Your hand:" << endl;
    for (const auto& c : playerHand)
        cout << c.rank << " of " << c.suit << " (" << c.value << ")" << endl;
    cout << "Hand value: " << calculateHandValue(playerHand) << endl;

    cout << "Dealer's visible card: " << dealerHand[0].rank << " of " << dealerHand[0].suit << endl;

    char choice;
    while (true) {
        cout << "Do you want to (h)it or (s)tand? ";
        cin >> choice;
        if (choice == 'h') {
            playerHand.push_back(deck.back());
            deck.pop_back();
            cout << "You drew " << playerHand.back().rank << " of " << playerHand.back().suit << endl;
            int playerValue = calculateHandValue(playerHand);
            cout << "Hand value: " << playerValue << endl;

            if (playerValue > 21) {
                cout << "\033[1;31m" << "You bust. Dealer wins!" << "\033[0m" << endl;
                cout << "Your budget: " << budget << endl;
                saveBudget(budget);
                return; 
            }
        }
        else if (choice == 's') {
            break;
        }
        else {
            cout << "Invalid choice. Please choose (h)it or (s)tand." << endl;
        }
    }

    cout << "Dealer's turn:" << endl;
    while (calculateHandValue(dealerHand) < 17) {
        dealerHand.push_back(deck.back());
        deck.pop_back();
        cout << "Dealer drew " << dealerHand.back().rank << " of " << dealerHand.back().suit << endl;
    }

    int playerValue = calculateHandValue(playerHand);
    int dealerValue = calculateHandValue(dealerHand);

    cout << "Your hand value: " << playerValue << endl;
    cout << "Dealer's hand value: " << dealerValue << endl;

    if (dealerValue > 21 || playerValue > dealerValue) {
        cout << "\033[1;32m" << "You win" << "\033[0m" << endl;
        budget += bet * 2;
        cout << "Your new budget: " << budget << endl;
        saveBudget(budget);
    }
    else if (playerValue == dealerValue) {
        cout << "\033[1;33m" << "It's a tie!" << "\033[0m" << endl;
        budget += bet;
        cout << "Your budget remains: " << budget << endl;
        saveBudget(budget);
    }
    else {
        cout << "\033[1;31m" << "Dealer wins!" << "\033[0m" << endl;
        cout << "Your budget: " << budget << endl;
        saveBudget(budget);
    }
}


int main() {
    srand(time(0));

    int game;
    int budget = loadBudget();
    cout << "==========================" << endl;
    cout << " Welcome to Casino Rush" << endl;
    cout << "==========================" << endl;
    cout << endl;

    cout << "\n1 - Slots\n";
    cout << "2 - Cube\n";
    cout << "3 - Plinko\n";
    cout << "4 - BlackJack\n";
    cin >> game;

    if (game == 1) {
        slots(budget);
    }
    else if (game == 2) {
        cube(budget);
    }
    else if (game == 3) {
        plinko(budget);
    }
    else if (game == 4) {
        blackjack(budget);
    }
    else {
        cout << "Invalid game choice.\n";
    }

    return 0;
}
