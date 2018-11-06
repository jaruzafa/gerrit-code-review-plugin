#!groovy

// Don't test plugin compatibility - exceeds 1 hour timeout
// Allow failing tests to retry execution
// buildPlugin(failFast: false)

// Test plugin compatbility to latest Jenkins LTS
// Allow failing tests to retry execution
try {
  buildPlugin(jenkinsVersions: [null, '2.60.1'], failFast: false, platforms: ['linux'])
  if (currentBuild.result == 'UNSTABLE') {
    review labels: [Verified: 0], message: "Build is unstable, there are failed tests ${env.BUILD_URL}"
  } else {
    review labels: [Verified: +1], message: "Build succeeded ${env.BUILD_URL}"
  }
} catch (e) {
  review labels: [Verified: -1], message: "Build failed ${env.BUILD_URL}"
}

def review(labels, message) {
  try {
    gerritReview labels: labels, message: message
  } catch (NoSuchMethodError e) {
  }
}
