 Real-Time Event Scheduling System
#include <iostream>
#include <queue>
#include <vector>
using namespace std;
struct Event {
    int priority;
    string eventName;
    string time;
    Event(int p, string e, string t) {
        priority = p;
        eventName = e;
        time = t;
    }
};
struct Compare {
    bool operator()(Event const& e1, Event const& e2) {
        return e1.priority > e2.priority;
    }
};
int main() {
    priority_queue<Event, vector<Event>, Compare> scheduler;
    int choice;
    do {
        cout << "\n===== REAL-TIME EVENT SCHEDULER =====\n";
        cout << "1. Add Event\n";
        cout << "2. Process Next Event\n";
        cout << "3. Display All Events\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        if(choice == 1) {
            string name, time;
            int priority;
            cin.ignore();
            cout << "Enter Event Name: ";
            getline(cin, name);
            cout << "Enter Event Time: ";
            getline(cin, time);
            cout << "Enter Priority (Low number = High priority): ";
            cin >> priority;
            scheduler.push(Event(priority, name, time));
            cout << "Event Added Successfully!\n";
        }
        else if(choice == 2) {
            if(scheduler.empty()) {
                cout << "No Events Available!\n";
            }
            else {
                Event next = scheduler.top();
                scheduler.pop();
                cout << "\nProcessing Event:\n";
                cout << "Event Name : " << next.eventName << endl;
                cout << "Time       : " << next.time << endl;
                cout << "Priority   : " << next.priority << endl;
            }
        }
        else if(choice == 3) {
            if(scheduler.empty()) {
                cout << "No Events Scheduled!\n";
            }
            else {
                priority_queue<Event, vector<Event>, Compare> temp = scheduler;
                cout << "\nScheduled Events:\n";
                while(!temp.empty()) {
                    Event e = temp.top();
                    cout << "Event : " << e.eventName
                         << " | Time : " << e.time
                         << " | Priority : " << e.priority << endl;
                    temp.pop();
                }
            }
        }
        else if(choice == 4) {
            cout << "Exiting Program...\n";
        }
        else {
            cout << "Invalid Choice!\n";
        }
    } while(choice != 4);
    return 0;
}
