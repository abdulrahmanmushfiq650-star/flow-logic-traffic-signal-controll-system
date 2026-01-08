# flow-logic-traffic-signal-controll-system
Project Description This project simulates a traffic signal control system using C++ programming. It demonstrates flow logic, conditional statements, and loop control to represent real-world traffic light behavior. The system cycles through Red, Yellow, and Green signals with fixed delays, displaying the current signal status on the console.

 
#include <iostream>
#include <string>
#include <vector>

using namespace std;

/* LogicFlow: Urban Intersection Controller
   Developed for CS101 - Discrete Mathematics
   Foundations: Rosen Chapters 1-2 (Propositional Logic)
*/

struct Lane {
    string name;
    bool hasVehicle;
    bool hasEmergency;
    bool pedestrianWaiting;
};

// Function to determine signal state using logical operators
// Logic: Green = Emergency OR (Vehicle AND NOT Pedestrian)
bool calculateSignal(bool p, bool q, bool r) {
    return r || (p && !q);
}

void runSimulation() {
    vector<Lane> intersection = {
        {"North-South Main", false, false, false},
        {"East-West Side", false, false, false}
    };

    cout << "--- LogicFlow Traffic Simulation ---" << endl;
    
    for (int i = 0; i < 2; i++) {
        int input;
        cout << "\nSettings for " << intersection[i].name << ":" << endl;
        cout << "Vehicle detected? (1=Yes, 0=No): "; cin >> input;
        intersection[i].hasVehicle = (input == 1);
        
        cout << "Pedestrian waiting? (1=Yes, 0=No): "; cin >> input;
        intersection[i].pedestrianWaiting = (input == 1);

        cout << "Emergency vehicle? (1=Yes, 0=No): "; cin >> input;
        intersection[i].hasEmergency = (input == 1);
    }

    cout << "\n--- LOGICAL DECISION OUTPUT ---" << endl;
    for (const auto& lane : intersection) {
        bool result = calculateSignal(lane.hasVehicle, lane.pedestrianWaiting, lane.hasEmergency);
        cout << "Lane: " << lane.name << " | Signal: " << (result ? "GREEN" : "RED") << endl;
        
        // Explain logic for the report
        if (lane.hasEmergency) cout << "  -> Reason: Emergency Override (r = True)" << endl;
        else if (result) cout << "  -> Reason: Traffic Flow Priority (p ^ !q = True)" << endl;
        else cout << "  -> Reason: Safety Halt (!result)" << endl;
    }
}

int main() {
    runSimulation();
    return 0;
}
