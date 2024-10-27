<script setup>
import Hero from '@/components/Hero.vue';
import Homecards from '@/components/HomeCards.vue';
import JobListings from '@/components/JobListings.vue';
</script>

<template>
    <Hero title="Muhammad Rashid Hussain" subtitle="Im a senior software engineer" />
    <Homecards />
    <JobListings :limit="3" :showButton="true" />
</template>