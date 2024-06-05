<template>
    <div class="loading-screen">
        <n-card title="Loading..." class="rounded-md">
            <n-progress type="line" :percentage="100" :show-indicator="false" processing />
        </n-card>
    </div>
</template>
