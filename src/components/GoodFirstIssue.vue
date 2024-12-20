<script setup lang="ts">
import { ref } from 'vue'

const issues = ref([]);
async function fetchGoodFirstIssues() {
    const response = await fetch('https://api.github.com/search/issues?q=is:issue+is:open+label:"good first issue"+language:JavaScript', {
        headers: {
            'Accept': 'application/vnd.github.v3+json'
        }
    });
    const data = await response.json();
    console.log(data);
    return data.items;
}

issues.value = await fetchGoodFirstIssues();

</script>

<template>
  <table>
    <thead>
        <tr>
            <th>
                Title
            </th>
            <th>
                Url
            </th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="issue in issues" :key="issue.id">
            <td>{issue.title}</td>
            <td>{issue.html_url}</td>
        </tr>
    </tbody>
    
  </table>
</template>

<style scoped>

</style>
