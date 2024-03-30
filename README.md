# dst
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* ExtractLetters(char const* str) {
    if (str == NULL) {
        return NULL;
    }

    int len = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        if ((str[i] >= 'A' && str[i] <= 'Z')  (str[i] >= 'a' && str[i] <= 'z')) {
            len++;
        }
    }

    char* result = (char*)malloc((len * 2) + 1 + len); // Увеличенный размер выделенной памяти
    if (result == NULL) {
        return NULL;
    }

    int index = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        if ((str[i] >= 'A' && str[i] <= 'Z')  (str[i] >= 'a' && str[i] <= 'z')) {
            result[index++] = str[i];
            result[index++] = ',';
            result[index++] = ' ';
        }
    }
    result[index] = '\0';
    return result;
}

char* ReadLine(void) {
    char* buffer = NULL;
    char tempBuffer[1000]; // Увеличенный размер буфера
    int length = 0;

    do {
        if (fgets(tempBuffer, sizeof(tempBuffer), stdin) == NULL) {
            break;
        }

        int tempLength = strlen(tempBuffer);
        char* newBuffer = (char*)realloc(buffer, length + tempLength + 1);
        if (newBuffer == NULL) {
            free(buffer);
            return NULL;
        }

        buffer = newBuffer;
        strcpy(buffer + length, tempBuffer);
        length += tempLength;
    } while (tempBuffer[strlen(tempBuffer) - 1] != '\n');

    return buffer;
}

int main() {
    char* input = ReadLine();
    while (strlen(input) > 0) {
        char* extractedLetters = ExtractLetters(input);
        if (extractedLetters != NULL) {
            printf("%s\n", extractedLetters);
            free(extractedLetters);
        }
        else {
            printf("Error: Failed to extract letters\n");
        }
        free(input);
        input = ReadLine();
    }

    free(input);
    return 0;
}
