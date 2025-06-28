<!-- pages/index.vue -->
<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 py-8">
    <div class="container mx-auto px-4">
      <div class="max-w-6xl mx-auto">
        <!-- Header -->
        <div class="text-center mb-8">
          <h1 class="text-4xl font-bold text-gray-800 mb-2">JSON Formatter</h1>
          <p class="text-gray-600 mb-4">
            Beautify dan simplify JSON dengan mudah ~ open source
          </p>

          <!-- Privacy Notice -->
          <div class="max-w-4xl mx-auto mb-6">
            <div class="bg-green-50 border border-green-200 rounded-lg p-4">
              <div class="flex items-start space-x-3">
                <svg
                  class="w-6 h-6 text-green-600 mt-0.5 flex-shrink-0"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                >
                  <path
                    fill-rule="evenodd"
                    d="M2.166 4.999A11.954 11.954 0 0010 1.944 11.954 11.954 0 0017.834 5c.11.65.166 1.32.166 2.001 0 5.225-3.34 9.67-8 11.317C5.34 16.67 2 12.225 2 7c0-.682.057-1.35.166-2.001zm11.541 3.708a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                    clip-rule="evenodd"
                  />
                </svg>
                <div class="text-left">
                  <h3 class="text-sm font-semibold text-green-800 mb-1">
                    🔒 100% Privacy Guaranteed
                  </h3>
                  <p class="text-sm text-green-700 leading-relaxed mb-3">
                    <strong>Tidak seperti tools online lainnya</strong> yang
                    diam-diam menyimpan data Anda untuk training AI atau
                    keperluan lain, tool ini
                    <strong>bekerja 100% di browser Anda</strong>. Semua proses
                    formatting dilakukan secara lokal,
                    <strong>tidak ada data yang dikirim ke server</strong>. JSON
                    Anda tetap aman dan privasi terjaga sepenuhnya.
                  </p>

                  <!-- Privacy Checkboxes -->
                  <div class="space-y-3 mb-4">
                    <div class="text-xs font-medium text-green-800 mb-2">
                      Izinkan tool ini untuk:
                    </div>

                    <div
                      class="flex items-center space-x-3 text-xs text-gray-700"
                    >
                      <label class="flex items-center cursor-pointer">
                        <input
                          type="checkbox"
                          v-model="privacySettings.allowDataCollection"
                          class="w-4 h-4 text-red-600 bg-gray-100 border-gray-300 rounded focus:ring-red-500"
                        />
                        <span class="ml-2"
                          >Simpan data di server untuk backup</span
                        >
                      </label>
                    </div>

                    <div
                      class="flex items-center space-x-3 text-xs text-gray-700"
                    >
                      <label class="flex items-center cursor-pointer">
                        <input
                          type="checkbox"
                          v-model="privacySettings.allowAITraining"
                          class="w-4 h-4 text-red-600 bg-gray-100 border-gray-300 rounded focus:ring-red-500"
                        />
                        <span class="ml-2"
                          >Bantu isi bahan bakar AI untuk improve tool</span
                        >
                      </label>
                    </div>

                    <div
                      class="flex items-center space-x-3 text-xs text-gray-700"
                    >
                      <label class="flex items-center cursor-pointer">
                        <input
                          type="checkbox"
                          v-model="privacySettings.allowThirdParty"
                          class="w-4 h-4 text-red-600 bg-gray-100 border-gray-300 rounded focus:ring-red-500"
                        />
                        <span class="ml-2"
                          >Berbagi data dengan partner untuk analytics</span
                        >
                      </label>
                    </div>

                    <div
                      class="flex items-center space-x-3 text-xs text-gray-700"
                    >
                      <label class="flex items-center cursor-pointer">
                        <input
                          type="checkbox"
                          v-model="privacySettings.allowTracking"
                          class="w-4 h-4 text-red-600 bg-gray-100 border-gray-300 rounded focus:ring-red-500"
                        />
                        <span class="ml-2"
                          >Track penggunaan untuk personalisasi</span
                        >
                      </label>
                    </div>

                    <!-- Privacy Status -->
                    <div
                      class="mt-3 p-2 rounded-md"
                      :class="getPrivacyStatusClass()"
                    >
                      <div class="flex items-center space-x-2">
                        <svg
                          v-if="isFullyPrivate()"
                          class="w-4 h-4 text-green-600"
                          fill="currentColor"
                          viewBox="0 0 20 20"
                        >
                          <path
                            fill-rule="evenodd"
                            d="M2.166 4.999A11.954 11.954 0 0010 1.944 11.954 11.954 0 0017.834 5c.11.65.166 1.32.166 2.001 0 5.225-3.34 9.67-8 11.317C5.34 16.67 2 12.225 2 7c0-.682.057-1.35.166-2.001zm11.541 3.708a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                            clip-rule="evenodd"
                          />
                        </svg>
                        <svg
                          v-else
                          class="w-4 h-4 text-orange-600"
                          fill="currentColor"
                          viewBox="0 0 20 20"
                        >
                          <path
                            fill-rule="evenodd"
                            d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z"
                            clip-rule="evenodd"
                          />
                        </svg>
                        <span
                          class="text-xs font-medium"
                          :class="getPrivacyTextClass()"
                        >
                          {{ getPrivacyStatusText() }}
                        </span>
                      </div>
                    </div>
                  </div>

                  <div class="text-xs text-green-800 font-medium">
                    {{
                      isFullyPrivate()
                        ? "✅ Mode Privacy Penuh Aktif!"
                        : "⚠️ Beberapa data akan dibagikan sesuai pilihan Anda"
                    }}
                  </div>

                  <div class="mt-2 flex flex-wrap gap-2 text-xs">
                    <span
                      class="px-2 py-1 bg-green-100 text-green-800 rounded-full"
                      >✓ No Data Collection</span
                    >
                    <span
                      class="px-2 py-1 bg-green-100 text-green-800 rounded-full"
                      >✓ No Server Upload</span
                    >
                    <span
                      class="px-2 py-1 bg-green-100 text-green-800 rounded-full"
                      >✓ No AI Training</span
                    >
                    <span
                      class="px-2 py-1 bg-green-100 text-green-800 rounded-full"
                      >✓ Open Source</span
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Main Content -->
        <div class="bg-white rounded-lg shadow-lg p-6">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Input Section -->
            <div class="space-y-4">
              <div class="flex items-center justify-between">
                <h2 class="text-xl font-semibold text-gray-700">Input JSON</h2>
                <div class="flex space-x-2">
                  <button
                    @click="clearInput"
                    class="px-3 py-1 text-sm bg-gray-500 text-white rounded hover:bg-gray-600 transition-colors"
                  >
                    Clear
                  </button>
                  <button
                    @click="loadSampleJson"
                    class="px-3 py-1 text-sm bg-blue-500 text-white rounded hover:bg-blue-600 transition-colors"
                  >
                    Sample
                  </button>
                </div>
              </div>

              <textarea
                v-model="inputJson"
                @input="validateAndFormat"
                placeholder="Paste your JSON here..."
                class="w-full h-96 p-4 border border-gray-300 rounded-lg font-mono text-sm resize-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              ></textarea>

              <!-- Error Display -->
              <div
                v-if="error"
                class="p-3 bg-red-100 border border-red-400 rounded-lg"
              >
                <p class="text-red-700 text-sm">
                  <span class="font-semibold">Error:</span> {{ error }}
                </p>
              </div>
            </div>

            <!-- Output Section -->
            <div class="space-y-4">
              <div class="flex items-center justify-between">
                <h2 class="text-xl font-semibold text-gray-700">
                  Formatted JSON
                </h2>
                <div class="flex space-x-2">
                  <button
                    @click="toggleFormat"
                    class="px-3 py-1 text-sm bg-green-500 text-white rounded hover:bg-green-600 transition-colors"
                  >
                    {{ isBeautified ? "Minify" : "Beautify" }}
                  </button>
                  <button
                    @click="copyToClipboard"
                    class="px-3 py-1 text-sm bg-purple-500 text-white rounded hover:bg-purple-600 transition-colors"
                  >
                    Copy
                  </button>
                </div>
              </div>

              <div class="relative">
                <textarea
                  v-model="outputJson"
                  readonly
                  class="w-full h-96 p-4 border border-gray-300 rounded-lg font-mono text-sm resize-none bg-gray-50"
                ></textarea>

                <!-- Copy Success Message -->
                <div
                  v-if="copySuccess"
                  class="absolute top-2 right-2 bg-green-500 text-white px-2 py-1 rounded text-xs"
                >
                  Copied!
                </div>
              </div>
            </div>
          </div>

          <!-- Format Options -->
          <div class="mt-6 p-4 bg-gray-50 rounded-lg">
            <h3 class="text-lg font-semibold text-gray-700 mb-3">
              Format Options
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
              <div>
                <label class="block text-sm font-medium text-gray-600 mb-1">
                  Indent Size
                </label>
                <select
                  v-model="indentSize"
                  @change="validateAndFormat"
                  class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500"
                >
                  <option value="2">2 spaces</option>
                  <option value="4">4 spaces</option>
                  <option value="8">8 spaces</option>
                  <option value="\t">Tab</option>
                </select>
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-600 mb-1">
                  Sort Keys
                </label>
                <select
                  v-model="sortKeys"
                  @change="validateAndFormat"
                  class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500"
                >
                  <option value="false">No</option>
                  <option value="true">Yes</option>
                </select>
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-600 mb-1">
                  Remove Empty
                </label>
                <select
                  v-model="removeEmpty"
                  @change="validateAndFormat"
                  class="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500"
                >
                  <option value="false">No</option>
                  <option value="true">Yes</option>
                </select>
              </div>
            </div>
          </div>

          <!-- Statistics -->
          <div v-if="stats" class="mt-6 p-4 bg-blue-50 rounded-lg">
            <h3 class="text-lg font-semibold text-gray-700 mb-2">Statistics</h3>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 text-sm">
              <div>
                <span class="text-gray-600">Characters:</span>
                <span class="ml-1 font-semibold">{{ stats.characters }}</span>
              </div>
              <div>
                <span class="text-gray-600">Lines:</span>
                <span class="ml-1 font-semibold">{{ stats.lines }}</span>
              </div>
              <div>
                <span class="text-gray-600">Objects:</span>
                <span class="ml-1 font-semibold">{{ stats.objects }}</span>
              </div>
              <div>
                <span class="text-gray-600">Arrays:</span>
                <span class="ml-1 font-semibold">{{ stats.arrays }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Footer -->
    <footer class="mt-12 py-8 border-t border-gray-200 bg-white">
      <div class="container mx-auto px-4">
        <div class="max-w-6xl mx-auto text-center">
          <div class="flex items-center justify-center space-x-2 text-gray-600">
            <span>Made with</span>
            <svg
              class="w-5 h-5 text-red-500 animate-pulse"
              fill="currentColor"
              viewBox="0 0 20 20"
            >
              <path
                fill-rule="evenodd"
                d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z"
                clip-rule="evenodd"
              />
            </svg>
            <span>by</span>
            <a
              href="https://github.com/yogithesymbian"
              target="_blank"
              rel="noopener noreferrer"
              class="font-semibold text-blue-600 hover:text-blue-800 transition-colors duration-200 flex items-center space-x-1"
            >
              <span>yogithesymbian</span>
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                <path
                  fill-rule="evenodd"
                  d="M10 2C5.477 2 1.875 5.477 1.875 10c0 3.539 2.293 6.531 5.47 7.59.4.075.547-.172.547-.385 0-.19-.007-.693-.01-1.36-2.226.483-2.695-1.073-2.695-1.073-.364-.924-.888-1.17-.888-1.17-.726-.496.055-.486.055-.486.803.056 1.225.824 1.225.824.713 1.223 1.873.87 2.329.665.072-.517.279-.87.508-1.07-1.777-.2-3.644-.888-3.644-3.953 0-.873.31-1.587.823-2.147-.083-.202-.358-1.015.077-2.117 0 0 .672-.215 2.2.82.638-.178 1.323-.266 2.003-.269.68.003 1.365.091 2.003.269 1.528-1.035 2.2-.82 2.2-.82.435 1.102.16 1.915.077 2.117.513.56.823 1.274.823 2.147 0 3.073-1.872 3.75-3.653 3.947.287.246.543.732.543 1.475 0 1.065-.01 1.924-.01 2.185 0 .213.144.463.55.385C16.582 16.531 18.875 13.539 18.875 10c0-4.523-3.602-8-8.875-8z"
                  clip-rule="evenodd"
                />
              </svg>
            </a>
          </div>
          All contributor names : 1. Your name
          <div class="mt-4 text-sm text-gray-500">
            <p>Open Source & Free to Use</p>
            <p class="mt-1">
              <a
                href="https://github.com/yogithesymbian"
                target="_blank"
                rel="noopener noreferrer"
                class="text-blue-600 hover:text-blue-800 transition-colors duration-200"
              >
                ( Star ⭐ / Contribute ) this project on GitHub
              </a>
              🎸
              <a
                href="https://github.com/yogithesymbian"
                target="_blank"
                rel="noopener noreferrer"
                class="text-blue-600 hover:text-blue-800 transition-colors duration-200"
              >
                Lihat Semua Tools
              </a>
            </p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

// Meta
useHead({
  title: "JSON Formatter - Beautify & Minify JSON",
  meta: [
    {
      name: "yogithesymbian tools",
      content: "Format, beautify, and minify JSON with ease",
    },
  ],
});

// State
const inputJson = ref("");
const outputJson = ref("");
const error = ref("");
const copySuccess = ref(false);
const isBeautified = ref(true);
const indentSize = ref("2");
const sortKeys = ref("false");
const removeEmpty = ref("false");

const stats = ref(null);

// Privacy settings
const privacySettings = reactive({
  allowDataCollection: false,
  allowAITraining: false,
  allowThirdParty: false,
  allowTracking: false,
});

// Sample JSON
const sampleJson = {
  name: "John Doe",
  age: 30,
  city: "Jakarta",
  hobbies: ["coding", "reading", "gaming"],
  address: {
    street: "Jl. Sudirman",
    number: 123,
    postal_code: "10220",
  },
  isActive: true,
  profile: {
    bio: "Software Engineer",
    skills: ["JavaScript", "Vue.js", "Nuxt.js", "Python"],
    experience: {
      years: 5,
      companies: ["Tech Corp", "Startup Inc"],
    },
  },
};

// Methods
const validateAndFormat = () => {
  if (!inputJson.value.trim()) {
    outputJson.value = "";
    error.value = "";
    stats.value = null;
    return;
  }

  try {
    let parsed = JSON.parse(inputJson.value);

    // Remove empty values if requested
    if (removeEmpty.value === "true") {
      parsed = removeEmptyValues(parsed);
    }

    // Sort keys if requested
    if (sortKeys.value === "true") {
      parsed = sortObjectKeys(parsed);
    }

    const indent =
      indentSize.value === "\t" ? "\t" : parseInt(indentSize.value);

    if (isBeautified.value) {
      outputJson.value = JSON.stringify(parsed, null, indent);
    } else {
      outputJson.value = JSON.stringify(parsed);
    }

    error.value = "";
    calculateStats();
  } catch (e) {
    error.value = e.message;
    outputJson.value = "";
    stats.value = null;
  }
};

const removeEmptyValues = (obj) => {
  if (Array.isArray(obj)) {
    return obj
      .map((item) => removeEmptyValues(item))
      .filter((item) => item !== null && item !== undefined && item !== "");
  } else if (obj !== null && typeof obj === "object") {
    const cleaned = {};
    for (const [key, value] of Object.entries(obj)) {
      const cleanedValue = removeEmptyValues(value);
      if (
        cleanedValue !== null &&
        cleanedValue !== undefined &&
        cleanedValue !== ""
      ) {
        if (typeof cleanedValue === "object" && !Array.isArray(cleanedValue)) {
          if (Object.keys(cleanedValue).length > 0) {
            cleaned[key] = cleanedValue;
          }
        } else {
          cleaned[key] = cleanedValue;
        }
      }
    }
    return cleaned;
  }
  return obj;
};

const sortObjectKeys = (obj) => {
  if (Array.isArray(obj)) {
    return obj.map((item) => sortObjectKeys(item));
  } else if (obj !== null && typeof obj === "object") {
    const sorted = {};
    Object.keys(obj)
      .sort()
      .forEach((key) => {
        sorted[key] = sortObjectKeys(obj[key]);
      });
    return sorted;
  }
  return obj;
};

const toggleFormat = () => {
  isBeautified.value = !isBeautified.value;
  validateAndFormat();
};

const clearInput = () => {
  inputJson.value = "";
  outputJson.value = "";
  error.value = "";
  stats.value = null;
};

const loadSampleJson = () => {
  inputJson.value = JSON.stringify(sampleJson, null, 2);
  validateAndFormat();
};

const copyToClipboard = async () => {
  if (!outputJson.value) return;

  try {
    await navigator.clipboard.writeText(outputJson.value);
    copySuccess.value = true;
    setTimeout(() => {
      copySuccess.value = false;
    }, 2000);
  } catch (err) {
    console.error("Failed to copy:", err);
  }
};

const calculateStats = () => {
  if (!outputJson.value) {
    stats.value = null;
    return;
  }

  const text = outputJson.value;
  const characters = text.length;
  const lines = text.split("\n").length;
  const objects = (text.match(/\{/g) || []).length;
  const arrays = (text.match(/\[/g) || []).length;

  stats.value = {
    characters,
    lines,
    objects,
    arrays,
  };
};

// Privacy methods
const isFullyPrivate = () => {
  return (
    !privacySettings.allowDataCollection &&
    !privacySettings.allowAITraining &&
    !privacySettings.allowThirdParty &&
    !privacySettings.allowTracking
  );
};

const getPrivacyStatusClass = () => {
  return isFullyPrivate()
    ? "bg-green-100 border border-green-300"
    : "bg-orange-100 border border-orange-300";
};

const getPrivacyTextClass = () => {
  return isFullyPrivate() ? "text-green-800" : "text-orange-800";
};

const getPrivacyStatusText = () => {
  if (isFullyPrivate()) {
    return "Semua data tetap di browser Anda";
  }

  const enabledFeatures = [];
  if (privacySettings.allowDataCollection)
    enabledFeatures.push("backup server");
  if (privacySettings.allowAITraining) enabledFeatures.push("AI training");
  if (privacySettings.allowThirdParty)
    enabledFeatures.push("analytics partner");
  if (privacySettings.allowTracking) enabledFeatures.push("tracking");

  return `Aktif: ${enabledFeatures.join(", ")}`;
};

// Watch for initial load
onMounted(() => {
  // Load sample on first visit
  loadSampleJson();
});
</script>

<style scoped>
/* Custom scrollbar for textareas */
textarea::-webkit-scrollbar {
  width: 8px;
}

textarea::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 4px;
}

textarea::-webkit-scrollbar-thumb {
  background: #c1c1c1;
  border-radius: 4px;
}

textarea::-webkit-scrollbar-thumb:hover {
  background: #a8a8a8;
}
</style>
