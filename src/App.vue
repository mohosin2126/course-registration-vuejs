<script setup>
import { onMounted, ref, computed } from "vue";

const courses = ref([]);
const selectedCourses = ref([]);
const totalCredits = ref(0);
const maxCredits = ref(18); // Assuming max credits is 18, adjust as needed

// Computed property for remaining credits
const remainingCredits = computed(() => {
  return maxCredits.value - totalCredits.value;
});

// Function to handle selecting a course
const handleSelectCourse = (course) => {
  // Check if course is already selected
  if (selectedCourses.value.some(c => c.id === course.id)) {
    alert("This course is already in your selection!");
    return;
  }

  // Check if adding this course would exceed credit limit
  if (totalCredits.value + course.creditInHours > maxCredits.value) {
    alert(`Cannot add course: would exceed maximum ${maxCredits.value} credits`);
    return;
  }

  // Add course to selected courses
  selectedCourses.value.push(course);
  totalCredits.value += course.creditInHours;
};

onMounted(async() => {
  try {
    const res = await fetch('./../../../public/data.json');
    const data = await res.json();
    courses.value = data;
    console.log(courses.value);
  } catch (error) {
    console.error("Error loading course data:", error);
  }
});
</script>

<template>
  <div class="w-2/3 mx-auto">
    <div>
      <h1 class="text-center mt-10 text-4xl font-bold">Course Registration</h1>
    </div>
    <div class="mt-20">
      <div>
        <div class="w-full flex flex-col md:flex-row gap-6">
          <!-- Course Cards Grid -->
          <div class="w-full md:w-2/3">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-6">
              <div
                  v-for="course in courses"
                  :key="course.id"
                  class="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow"
              >
                <img
                    class="w-full h-48 object-cover"
                    :src="course.image"
                    :alt="course.title"
                />
                <div class="p-4">
                  <h2 class="text-xl font-bold text-gray-800 mb-2">{{ course.title }}</h2>
                  <p class="text-gray-600 text-sm mb-4 line-clamp-3">{{ course.description }}</p>
                  <div class="flex justify-between items-center mb-4">
                    <div class="flex items-center">
                      <img :src="course.dollarIcon" alt="Price" class="w-5 h-5 mr-1" />
                      <span class="text-gray-700">${{ course.price }}</span>
                    </div>
                    <div class="flex items-center">
                      <img :src="course.bookIcon" alt="Credit" class="w-5 h-5 mr-1" />
                      <span class="text-gray-700">{{ course.creditInHours }} Credits</span>
                    </div>
                  </div>
                  <button
                      @click="handleSelectCourse(course)"
                      class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded transition-colors"
                  >
                    Select Course
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Selected Course Summary -->
          <div class="w-full md:w-1/3">
            <div class="bg-white rounded-lg shadow-md p-6 sticky top-6">
              <h2 class="text-xl font-bold text-blue-600 mb-4">Course Summary</h2>
              <div class="border-b pb-4 mb-4">
                <h3 class="text-lg font-semibold text-gray-800 mb-2">
                  Credit Information
                </h3>
                <div class="flex justify-between items-center mb-2">
                  <span class="text-gray-600">Total Credit:</span>
                  <span class="font-medium">{{ totalCredits }} hours</span>
                </div>
                <div class="flex justify-between items-center mb-2">
                  <span class="text-gray-600">Credit Remaining:</span>
                  <span class="font-medium">{{ remainingCredits }} hours</span>
                </div>
              </div>

              <h3 class="text-lg font-semibold text-gray-800 mb-3">
                Selected Courses: {{ selectedCourses.length }}
              </h3>

              <ul v-if="selectedCourses.length > 0" class="space-y-3">
                <li
                    v-for="(course, index) in selectedCourses"
                    :key="course.id"
                    class="flex items-center bg-gray-50 p-3 rounded-md"
                >
                  <span class="mr-2 text-gray-500">{{ index + 1 }}.</span>
                  <span class="text-gray-800">{{ course.title }}</span>
                </li>
              </ul>
              <p v-else class="text-gray-500 italic">No courses selected yet</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>