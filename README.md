# Adjacency

#include <stdio.h>

#define V 4  

int main() {
    int adj[V][V] = {0};  

  
    adj[0][1] = adj[1][0] = 1; // A-B
    adj[0][2] = adj[2][0] = 1; // A-C
    adj[1][3] = adj[3][1] = 1; // B-D

    printf("Adjacency Matrix (Undirected):\n");
    printf("    A B C D\n");
    for (int i = 0; i < V; i++) {
        printf("%c | ", 'A' + i);
        for (int j = 0; j < V; j++) {
            printf("%d ", adj[i][j]);
        }
        printf("\n");
    }

    return 0;
}
-------------------------------------------------
#include <stdio.h>
#include <stdlib.h>

#define V 4  

struct Node {
    int dest;
    struct Node* next;
};

struct Graph {
    struct Node* adj[V];
};

struct Node* newNode(int dest) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->dest = dest;
    node->next = NULL;
    return node;
}


void addEdge(struct Graph* g, int u, int v) {
    struct Node* node = newNode(v);
    node->next = g->adj[u];
    g->adj[u] = node;
}

// Print the adjacency list
void printGraph(struct Graph* g) {
    printf("Adjacency List (Directed):\n");
    for (int i = 0; i < V; i++) {
        printf("%c -> ", 'A' + i);
        struct Node* temp = g->adj[i];
        while (temp) {
            printf("%c ", 'A' + temp->dest);
            temp = temp->next;
        }
        printf("\n");
    }
}

int main() {
    struct Graph g = {0};

 
    addEdge(&g, 0, 1); // A->B
    addEdge(&g, 0, 2); // A->C
    addEdge(&g, 1, 3); // B->D

    printGraph(&g);

    return 0;
}
