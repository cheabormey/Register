<template>
  <div class="max-w-[1640px] mx-auto p-4">
    <h1 class="text-center text-3xl">Registration</h1>
    <br />
    <!-- input -->
    <div class="max-w-lg mx-auto text-[13px]">
      <FloatLabel>
        <InputText
          class="w-full border-slate-300 border-2 p-2 bg-slate-100"
          id="username"
          v-model="formData.username"
        />
        <label for="username">Name</label>
      </FloatLabel>
      <br />
      <FloatLabel>
        <InputText
          class="w-full border-slate-300 border-2 p-2 bg-slate-100"
          id="phoneNumber"
          v-model="formData.phoneNumber"
        />
        <label for="phoneNumber">Phone number</label>
      </FloatLabel>
      <br />
      <FloatLabel>
        <InputText
          class="w-full border-slate-300 border-2 p-2 bg-slate-100"
          id="address"
          v-model="formData.address"
        />
        <label for="address">Address</label>
      </FloatLabel>
      <br />
      <FloatLabel>
        <InputText
          class="w-full border-slate-300 border-2 p-2 bg-slate-100"
          id="company"
          v-model="formData.company"
        />
        <label for="company">Company</label>
      </FloatLabel>
    </div>
    <br />
    <!-- date -->
    <div class="flex gap-4 justify-center">
      <!-- days -->
      <div class="w-full sm:w-auto">
        <Dropdown
          v-model="formData.selectedDay"
          :options="days"
          optionLabel="name"
          placeholder="Day"
          class="w-full border-2 border-slate-200 rounded-lg"
        />
      </div>
      <!-- months -->
      <div class="w-full sm:w-auto">
        <Dropdown
          v-model="formData.selectedMonth"
          :options="months"
          optionLabel="name"
          placeholder="Month"
          class="w-full border-2 border-slate-200 rounded-lg"
        />
      </div>
      <!-- Year -->
      <div class="w-full sm:w-auto">
        <Dropdown
          v-model="formData.selectedYear"
          :options="years"
          optionLabel="name"
          placeholder="Year"
          class="w-full border-2 border-slate-200 rounded-lg"
        />
      </div>
    </div>
    <br />
    <!-- button submit -->
    <div class="flex justify-center">
      <button  type="button" class="bg-sky-400 p-2 rounded-lg" @click="submitForm" severity="success">
        Submit
      </button>


      
    </div>
    <br />
    <!-- data table -->
    <div v-if="dataList.length > 0" class="overflow-x-auto">
      <table class="min-w-full bg-white">
        <thead>
          <tr class="bg-teal-950 text-orange-100 ">
            <th class="px-4 py-2">Name</th>
            <th class="px-4 py-2">Phone Number</th>
            <th class="px-4 py-2">Address</th>
            <th class="px-4 py-2">Company</th>
            <th class="px-4 py-2">Day</th>
            <th class="px-4 py-2">Month</th>
            <th class="px-4 py-2">Year</th>
            <th class="px-4 py-2">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in dataList" :key="index">
            <td class="border px-4 py-2">{{ item.username }}</td>
            <td class="border px-4 py-2">{{ item.phoneNumber }}</td>
            <td class="border px-4 py-2">{{ item.address }}</td>
            <td class="border px-4 py-2">{{ item.company }}</td>
            <td class="border px-4 py-2">{{ item.selectedDay.name }}</td>
            <td class="border px-4 py-2">{{ item.selectedMonth.name }}</td>
            <td class="border px-4 py-2">{{ item.selectedYear.name }}</td>
            <td class="border px-4 py-2 text-center justify-between">
              <!-- button edit -->
              <button @click="editItem(index)" class="">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                  class="size-6 text-blue-700"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10"
                  />
                </svg>
              </button>
              <!-- button delete -->
              <button @click="deleteItem(index)" class="">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                  class="size-6 text-red-600"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0"
                  />
                </svg>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import InputText from "primevue/inputtext";
import FloatLabel from "primevue/floatlabel";
import Dropdown from "primevue/dropdown";

export default {
  components: {
    InputText,
    FloatLabel,
    Dropdown,
  },
  setup() {
    const formData = ref({
      username: "",
      phoneNumber: "",
      address: "",
      company: "",
      selectedDay: null,
      selectedMonth: null,
      selectedYear: null,
    });

    const days = ref(
      Array.from({ length: 31 }, (_, i) => ({ name: `${i + 1}`, code: `${i + 1}` }))
    );

    const months = ref([
      { name: "January", code: "Jan" },
      { name: "February", code: "Feb" },
      { name: "March", code: "Mar" },
      { name: "April", code: "Apr" },
      { name: "May", code: "May" },
      { name: "June", code: "Jun" },
      { name: "July", code: "Jul" },
      { name: "August", code: "Aug" },
      { name: "September", code: "Sep" },
      { name: "October", code: "Oct" },
      { name: "November", code: "Nov" },
      { name: "December", code: "Dec" },
    ]);

    const years = ref(
      Array.from({ length: 125 }, (_, i) => {
        const year = 1900 + i;
        return { name: `${year}`, code: `${year}` };
      })
    );

    const dataList = ref([]);
    const isEditing = ref(false);
    const currentEditIndex = ref(null);

    const submitForm = () => {
      if (isEditing.value) {
        // Update existing entry
        dataList.value[currentEditIndex.value] = { ...formData.value };
        isEditing.value = false;
        currentEditIndex.value = null;
      } else {
        // Add new entry
        dataList.value.push({ ...formData.value });
      }
      resetForm();
    };

    const deleteItem = (index) => {
      dataList.value.splice(index, 1);
    };

    const editItem = (index) => {
      formData.value = { ...dataList.value[index] };
      isEditing.value = true;
      currentEditIndex.value = index;
    };

    const resetForm = () => {
      formData.value = {
        username: "",
        phoneNumber: "",
        address: "",
        company: "",
        selectedDay: null,
        selectedMonth: null,
        selectedYear: null,
      };
    };

    return {
      formData,
      days,
      months,
      years,
      dataList,
      submitForm,
      deleteItem,
      editItem,
      resetForm,
    };
  },
};
</script>

<style scoped>
.table-container {
  overflow-x: auto;
}
</style>
