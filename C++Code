//read in a text file of interconnected cities.
//get user input for from/to
//give list of potential cities if input is partial
//find and display shortest route to get from start to finish

#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <queue>
#include <list>
using namespace std;

//pull city names from file
 int processFile(string cityName[], string f); 

 //pull city from/to info from file
 void createVector(vector<int> arr[], string cityName[], int size, string fileName);
 
 //get user input, will return list of potential inputs if no match
 int getUserInput(string seek, string cityName[], int size);
 
 //Dijkstras algorithm implementation
 void bfs (vector<int> alists[], int size, int start, int target,string arr[]);

 int main(){
	string fileName;
	int startCity;
	int endCity;
	string temp;
	bool running = true;
	cout << "Enter filename:";
	cin >> fileName;
	
	string cityNames[150];
	vector<int> connections[150];
	int size = processFile(cityNames,fileName);
	createVector(connections, cityNames, size,fileName);
	while(running){
	cout << "Enter starting city: ";
	cin >> fileName;
	startCity = getUserInput(fileName,cityNames,size);
	cout << "\nEnter destination city: ";
	cin >> fileName;
	endCity = getUserInput(fileName,cityNames,size);
	bfs(connections,size,startCity,endCity,cityNames);
	cout << "\b\b\b\b";
	cout << "\nSearch again? Y or N";
	cin >> fileName;
	if(fileName == "N")
		running = false;
	}
}


bool checkArr(string cityName[], string city, int size){
	for(int i = 0;i<size;i++){
		if(cityName[i] == city){
			return false;
		}
	}
	cityName[size] = city;
	return true;
}

//open file first time
//parse file into strings and push them into array
//return # of cities in array
 int processFile(string cityName[], string f){
	ifstream inFile(f);
	string currCity;
	int size = 0;
	while(getline(inFile,currCity)){
		currCity = currCity.substr(7,currCity.length());
		if(checkArr(cityName,currCity,size))
			size++;
	}
	return size;
 }

//find index of City in array
 int getIndex(string cityName[],string seekCity, int size){
	for(int i = 0;i<size;i++){
		if(cityName[i] == seekCity){
			return i;
		}
	}
	return -1;
 }

 //open file again, for each city starting with the word "from:" find it in array cityName
 //then push_back of vector at that index with the index of the connected city
 //until next "from:" encountered
 void createVector(vector<int> cityConnection[], string cityName[], int size, string fileName){
	ifstream inFile(fileName);
	string currCity;
	int currIndex;
	int pushIndex;
	size_t checkFrom;
	
	//make sure at start of file
	inFile.clear();
	inFile.seekg(0,inFile.beg);
	
	while(getline(inFile,currCity)){
		//check if line starts with "From:"
		checkFrom = currCity.find("From:");
		if(checkFrom != string::npos){
			//from was found in string, means new city/new index needed;
			currCity = currCity.substr(7,currCity.length());
			currIndex = getIndex(cityName, currCity,size);
		}
		//no from found, get city index, push that into vector at current index
		else if(checkFrom == string::npos){
			currCity = currCity.substr(7,currCity.length());
			pushIndex = getIndex(cityName,currCity,size);
			cityConnection[currIndex].push_back(pushIndex);
			
		}
	}
 }

//check arr of strings for exact match, if not then assemble list of potentials and have them pick one, then get index of that city and return it
 int getUserInput(string seek,string cityName[],int size){
	int x = getIndex(cityName,seek,size);
	cout << x;
	if(x != -1){
		return x;
	}
	else{
		//get an array of potential inputs
		string potentials[100];
		int y = 0;
		for(int i = 0;i<size;i++){
			if(cityName[i].find(seek) != string::npos){
			potentials[y] = cityName[i];
			y++;
			}
		}
		cout << "\nNo match, potential matches found: " << y;
		cout << "\nPlease choose number you meant.";
		for(int i = 0;i<y;i++){
			cout << i+1 << ". " << potentials[i] << "\n";
			

		}
		cin >> y;
		int x = getIndex(cityName,potentials[y-1],size);
		return x;
	}
}


 
 void printPath(int parents[], int size, int startv, int endv, string arr[]) {
	if (endv != startv) {
		printPath(parents, size, startv, parents[endv], arr);

	}
	cout << arr[endv] << " -> ";
}
	
	
void bfs (vector<int> alists[], int size, int start, int target, string arr[]) {
	int * parents = new int[size];
	for (int i = 0; i< size; i++) parents[i] = -1;
	parents[start] = start;
	queue<int> q;
	q.push(start);
	bool found = false;
	while (!q.empty() && !found) {
		int v = q.front();
		q.pop();
		if (v == target) 
			found = true;
			
		else for (int i = 0; i < alists[v].size(); i++) {
			int w = alists[v][i];
			if (parents[w] == -1) {
				parents[w] = v;
				q.push(w);
			}
		}
	}
	if (found) 			
		printPath(parents,10,start,target,arr);  
	else 
		cout << "Not found";
	cout << endl;
	delete [] parents;
}
