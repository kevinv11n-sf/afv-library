---
name: salesforce-experience-site
description: Generate Digital Experience Site metadata including Network, CustomSite, and DigitalExperienceBundle configurations. Use when creating Experience Cloud sites or web apps.
---

## When to Use This Skill

Use this skill when you need to:
- Create Experience Cloud sites or communities
- Build customer-facing portals
- Set up site configuration and settings
- Generate Experience Site metadata
- Troubleshoot deployment errors related to Experience Sites

## Specification

# Digital Experience Site Metadata Specification

## 📋 Overview
Digital Experience Sites for building and hosting websites backed by either Salesforce or web app (React) metadata.

## 🎯 Purpose
- Provide a website for retail and customer services.
- Use either Salesforce Experience metadata or something else like React or Angular.
- Configure site, network, and app settings for the website.

## ⚙️ Required Properties
### Core Site Properties
- **siteName**: You must determine the name of the site. You must make the name `UpperCamelCase` (e.g., `'MyCommunity'`).
- **siteUrlPathPrefix**. You must determine the url path prefix of the site. You must make the url path prefix `kebab-case`. You must convert the site name to the url prefix if an explicit prefix is not provided (e.g., `'my-community'`).
- **templateType**: You must determine what type of template is being used for the site. Default to `OneRuntime`.

## 🔧 Site Template Types
### OneRuntime
- **Purpose**: Support a site or web app backed by a non-Salesforce metadata framework like React or Angular

## 🔄 Generation Workflow
You must follow the steps below to generate insertable Digital Experience Site metadata.

### Step 1: Determine the Template Type
- You must first determine the template type of the Experience Site using the Site Template Types section.

### Step 2: Use Template Type to Get Metadata Configurations for Project Structure and Fields
- You must determine the project structure and fields for the chosen template type.
- You must resolve all properties and fields.
- You must use the following configurations for OneRuntime template type:

#### OneRuntime Template Type Configuration
#### Project Structure
#### Additional Instructions
- You must construct the project folders to match the provided paths.
- You must use the `get_metadata_api_context` MCP tool to get the schemas for `DigitalExperienceConfig`, `DigitalExperienceBundle`, `Network`, and `CustomSite`.

#### Configuration
- DigitalExperienceConfig
    - Path: `digitalExperienceConfigs/{siteName}1.digitalExperienceConfig`
- DigitalExperienceBundle
    - Path: `digitalExperiences/site/{siteName}1/{siteName}1.digitalExperience-meta.xml`
- Network
    - Path: `networks/{siteName}.network`
- CustomSite
    - Path: `sites/{siteName}.site`
- DigitalExperience
    - Path: `digitalExperiences/site/{siteName}1/{contentType}/{apiName}/*`
    - Description: These are the content component directories defining site and language information. Each directory must have a `_meta.json` and `content.json` file.
    - Required component content types (`contentType`):
        - `sfdc_cms__site`

#### Fields
#### Additional Site Properties
- **namespace**: You must determine the namespace of the React app. Default to empty.
- **appDevName**. You must determine the developer name of the React app. Default to empty.

#### Configuration
- `DigitalExperienceConfig`
    - label: {siteName}
    - urlPathPrefix: {siteUrlPathPrefix}
    - space: site/{siteName}1

- `DigitalExperienceBundle`
    - label: {siteName}1

- `Network`
    - allowInternalUserLogin: false
    - allowMembersToFlag: false
    - changePasswordTemplate: unfiled$public/CommunityChangePasswordEmailTemplate
    - disableReputationRecordConversations: true
    - emailSenderAddress: admin@company.com
    - emailSenderName: {siteName}
    - embeddedLoginEnabled: false
    - enableApexCDNCaching: true
    - enableCustomVFErrorPageOverrides: false
    - enableDirectMessages: true
    - enableExpFriendlyUrlsAsDefault: false
    - enableExperienceBundleBasedSnaOverrideEnabled: true
    - enableGuestChatter: false
    - enableGuestFileAccess: false
    - enableGuestMemberVisibility: false
    - enableImageOptimizationCDN: true
    - enableInvitation: false
    - enableKnowledgeable: false
    - enableLWRExperienceConnectedApp: true
    - enableMemberVisibility: false
    - enableNicknameDisplay: true
    - enablePrivateMessages: false
    - enableReputation: false
    - enableShowAllNetworkSettings: false
    - enableSiteAsContainer: true
    - enableTalkingAboutStats: true
    - enableTopicAssignmentRules: true
    - enableTopicSuggestions: false
    - enableUpDownVote: false
    - forgotPasswordTemplate: unfiled$public/CommunityForgotPasswordEmailTemplate
    - gatherCustomerSentimentData: false
    - headlessForgotPasswordTemplate: unfiled$public/CommunityHeadlessForgotPasswordTemplate
    - headlessRegistrationTemplate: unfiled$public/CommunityHeadlessRegistrationTemplate
    - networkMemberGroups:
        - profile: admin
    - networkPageOverrides:
        - changePasswordPageOverrideSetting: Standard
        - forgotPasswordPageOverrideSetting: Designer
        - homePageOverrideSetting: Designer
        - loginPageOverrideSetting: Designer
        - selfRegProfilePageOverrideSetting: Designer
    - newSenderAddress: admin@company.com
    - picassoSite: {siteName}1
    - selfRegistration: false
    - sendWelcomeEmail: true
    - site: {siteName}
    - siteArchiveStatus: NotArchived
    - status: UnderConstruction
    - tabs:
        - defaultTab: home
        - standardTab: Chatter
    - urlPathPrefix: {siteUrlPathPrefix}vforcesite
    - welcomeTemplate: unfiled$public/CommunityWelcomeEmailTemplate

- `CustomSite`
    - active: true
    - allowGuestPaymentsApi: false
    - allowHomePage: false
    - allowStandardAnswersPages: false
    - allowStandardIdeasPages: false
    - allowStandardLookups: false
    - allowStandardPortalPages: true
    - allowStandardSearch: false
    - authorizationRequiredPage: CommunitiesLogin
    - bandwidthExceededPage: BandwidthExceeded
    - browserXssProtection: true
    - cachePublicVisualforcePagesInProxyServers: true
    - clickjackProtectionLevel: SameOriginOnly
    - contentSniffingProtection: true
    - enableAuraRequests: true
    - fileNotFoundPage: FileNotFound
    - genericErrorPage: Exception
    - inMaintenancePage: InMaintenance
    - indexPage: CommunitiesLanding
    - masterLabel: {siteName}
    - redirectToCustomDomain: false
    - referrerPolicyOriginWhenCrossOrigin: true
    - selfRegPage: CommunitiesSelfReg
    - siteType: ChatterNetwork
    - urlPathPrefix: {siteUrlPathPrefix}vforcesite

- `DigitalExperience`
    1. sfdc_cms__site
        - apiName: {siteName}1
        - type: sfdc_cms__site
        - title: {siteName}
        - urlName: {siteUrlPathPrefix}
        - contentBody:
            - authenticationType: AUTHENTICATED_WITH_PUBLIC_ACCESS_ENABLED
            - appContainer: true
            - appSpace: {namespace}__{appDevName}

### Step 3: Create a Project Structure for the Chosen Template Type
You must construct a metadata project folder using the knowledge from Step 2.

### Step 4: Resolve All Required Fields for the Chosen Template Type
You must determine values for all required metadata fields using the knowledge from Step 2.

## ✅ Verification Checklist
- [ ] All properties are resolved.
- [ ] All metadata directories and files are created based on the template type configurations.
- [ ] All metadata fields are populated based on the template type configurations.
- [ ] All metadata is validated by running CLI command `sf project deploy validate --metadata DigitalExperienceBundle DigitalExperience DigitalExperienceConfig Network CustomSite --target-org ${usernameOrAlias}`
