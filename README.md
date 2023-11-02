// heap_sort
// heap_sort sıralama algoritması kullanılarak 1'den 100'e kadar rastgele tam sayılarla oluşturulan dizinin sıralanması
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>

// Max heap yapısını korumak için aşağıdaki fonksiyonlar tanımlanır.

// Verilen dizinin i. öğesini aşağı doğru yerleştirir ve max heap yapısını korur.
void maxHeapify(int arr[], int n, int i) {
    int largest = i; // Kök düğüm
    int left = 2 * i + 1; // Sol alt düğüm
    int right = 2 * i + 2; // Sağ alt düğüm

    // Sol alt düğüm, kök düğümden daha büyükse largest'ı güncelle
    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    // Sağ alt düğüm, largest'tan daha büyükse largest'ı güncelle
    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    // largest, kök düğüm değilse yer değiştirme yap ve max heap yapısını koru
    if (largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;

        // Değişiklik yapılan alt ağaç üzerinde maxHeapify fonksiyonunu tekrar çağır
        maxHeapify(arr, n, largest);
    }
}

// Heap Sort işlemi
void heapSort(int arr[], int n) {
    // Max heap yapısını oluştur
    int i;
    for (i = n / 2 - 1; i >= 0; i--) {
        maxHeapify(arr, n, i);
    }

    // Diziyi sırala
    for (i = n - 1; i > 0; i--) {
        // Kök düğümü son düğümle değiştir
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;

        // Max heap yapısını koru (sıralanmış kısmı hariç tut)
        maxHeapify(arr, i, 0);
    }
}

int main() {
    //int arr[] = {12, 11, 13, 5, 6, 7};
    srand(time(NULL));
	int girilen_sayi_adedi=100;
    int arr[100] = {0};
    int n = sizeof(arr) / sizeof(arr[0]); //dizi boyutunun hesaplanması
    int i;
    
    for(i=0; i<girilen_sayi_adedi;i++) //diziye rastgele eleman atama
    {
    	arr[i] = rand()%girilen_sayi_adedi+1;
	}

    printf("Siralanmamis dizi: \n");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    heapSort(arr, n);

    printf("Siralanmis dizi: \n");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
