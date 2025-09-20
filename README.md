# 92.-Team-Cygnus-Develop an assistant that detects phishing attempts from emails, screenshots, or messages,
and guides users to respond safely-
#include <stdio.h>
#include <string.h>

int main() {
    char msg[1000];
    printf("Enter the message/email:\n");
    fgets(msg, sizeof(msg), stdin);
    int score = 0;
    int urlFound = 0;
    // Check for phishing keywords
    if (strstr(msg, "password") || strstr(msg, "verify") || strstr(msg, "urgent"))
        score += 5;
    if (strstr(msg, "click") || strstr(msg, "login") || strstr(msg, "bank"))
        score += 5;
    if (strstr(msg, "lottery") || strstr(msg, "prize") || strstr(msg, "free") || strstr(msg, "congratulations"))
        score += 5;
    // Check for suspicious URLs
    if (strstr(msg, "http://") || strstr(msg, "https://")) {
        score += 5;
        urlFound = 1;
        if (strstr(msg, "192.") || strstr(msg, ".xyz") || strstr(msg, ".zip"))
            score += 5;
    }
    // Print results
    printf("\n--- Analysis Result ---\n");
    printf("Risk Score: %d / 20\n", score);
    if (score >= 10) {
        printf("Risk Level: DANGEROUS\n");
        if (urlFound) printf(" Suspicious link detected!\n");
        printf("Advice: Do NOT click links, verify sender, and report.\n");
    } else if (score >= 5) {
        printf("Risk Level: SUSPICIOUS\n");
        if (urlFound) printf(" Contains a link — check carefully.\n");
        printf("Advice: Be cautious, double-check sender before acting.\n");
    } else {
        printf("Risk Level: SAFE (No major red flags)\n");
        printf("Advice: Stay alert even safe-looking emails may hide threats.\n");
    }

    return 0;
}
