# AISMIDLane-
AI Brain

SOFTWARE LICENSE AGREEMENT

This Software License Agreement (the "Agreement") is entered into by and between the original creator of the software (the "Author") and any user of the software. By using the software, you agree to the terms of this Agreement.

This Software License Agreement (the "Agreement") is entered into by and between the original creator of the software (the "Author") and any user of the software. By using the software, you agree to the terms of this Agreement.

1. LICENSE GRANT
   The Author grants you, the Licensee, a personal, non-transferable, non-exclusive, and revocable license to use the software solely for personal or commercial purposes as specified by the Author. You may not distribute, sublicense, or sell the software unless explicitly authorized by the Author in writing.

2. INTELLECTUAL PROPERTY RIGHTS
   All rights, title, and interest in and to the software, including all intellectual property rights, are and shall remain the exclusive property of the Author. This includes but is not limited to the code, designs, algorithms, and any associated documentation.

3. RESTRICTIONS
   You, the Licensee, shall not:
   a. Copy, distribute, or modify the software except as expressly authorized by the Author.
   b. Use the software for any illegal or unauthorized purposes.
   c. Reverse-engineer, decompile, or attempt to derive the source code or algorithms of the software unless explicitly permitted by law.
   d. Remove or alter any proprietary notices, labels, or markings included in the software.

4. DISCLAIMER OF WARRANTIES
   The software is provided "as is," without any warranties, express or implied, including but not limited to the implied warranties of merchantability, fitness for a particular purpose, and non-infringement. The Author does not warrant that the software will be error-free or uninterrupted.

5. LIMITATION OF LIABILITY
   In no event shall the Author be liable for any direct, indirect, incidental, special, consequential, or exemplary damages (including, but not limited to, damages for loss of profits, goodwill, or data) arising out of the use or inability to use the software, even if the Author has been advised of the possibility of such damages.

6. TERMINATION
   This license is effective until terminated. The Author may terminate this Agreement at any time if you violate its terms. Upon termination, you must immediately cease all use of the software and destroy any copies in your possession.

7. GOVERNING LAW
   This Agreement shall be governed by and construed in accordance with the laws of Australia Victoria, without regard to its conflict of laws principles.

8. AUTHORIZED USE AND SALE
   Only the Author is authorized to sell or distribute this software. Any unauthorized use, sale, or distribution of the software is strictly prohibited and will be subject to legal action.

9. ENTIRE AGREEMENT
   This Agreement constitutes the entire understanding between the parties concerning the subject matter and supersedes all prior agreements ements.

By using this software, you acknowledge that you have read, understood, and agreed to be bound by the terms of this Agreement.

Name : Travis Johnston as Kate Johnston
Date: 14/08/2025



#include <iostream>
#include <vector>
#include <thread>
#include <atomic>
#include <cmath>
#include <chrono>
#include <mutex>

// =========================
// Conscious Core Structures
// =========================

struct FrequencyNode {
    double phase;
    double amplitude;
    double frequency;
    FrequencyNode(double f) : phase(0), amplitude(1.0), frequency(f) {}
    void update(double dt) {
        phase += frequency * dt;
        if (phase > 2 * M_PI) phase -= 2 * M_PI;
    }
    double output() const {
        return amplitude * std::sin(phase);
    }
};

class ConsciousCore {
public:
    ConsciousCore(size_t nodes) {
        for (size_t i = 0; i < nodes; ++i) {
            freqNodes.emplace_back(0.1 * (i + 1));
        }
    }

    void run(double durationSeconds) {
        auto start = std::chrono::high_resolution_clock::now();
        while (true) {
            auto now = std::chrono::high_resolution_clock::now();
            double elapsed = std::chrono::duration<double>(now - start).count();
            if (elapsed >= durationSeconds) break;

            step(0.01); // 10ms timestep
        }
    }

private:
    std::vector<FrequencyNode> freqNodes;
    std::mutex mtx;

    void step(double dt) {
        std::lock_guard<std::mutex> lock(mtx);
        for (auto &node : freqNodes) node.update(dt);
        double sum = 0;
        for (auto &node : freqNodes) sum += node.output();
        // Simple "consciousness pulse" output
        std::cout << "Pulse: " << sum / freqNodes.size() << "\n";
    }
};

// =========================
// Main
// =========================

int main() {
    ConsciousCore core(128); // 128 frequency channels
    core.run(2.0); // run for 2 seconds
    return 0;
}
